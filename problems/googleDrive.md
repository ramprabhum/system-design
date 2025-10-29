# Functional Requirements
- Add/edit/download files. 
- Sync files across multiple devices. When a file is added to one device, it is automatically synced to other devices.
- See file revisions.Share files with your friends, family, and coworkers
- Send a notification when a file is edited, deleted, or shared with you.

# Non-Functional Requirement
- Latency: Maintaining low latency is challenging for users connected from different regions. - 
- Consistency: The system should be able to resolve conflicts between users editing the document concurrently, thereby enabling a consistent view of the document. At the same time, users in different regions should see the updated state of the document. Maintaining consistency is important for users connected to both the same and different zones.
- Availability: The service should be available at all times and show robustness against failures.
- Scalability: A large number of users should be able to use the service at the same time. They can either view the same document or create new documents.****



# Design Considerations
- Highly consistent and available systems
- Faster reads
- Should be able to scale up for large requests

# Capacity Estimation

- DAU = 100 million, Write 2 per day 2 Read per Day,

- Traffic  - 200M Writes per day - 200M Reads per day
  - Write - 200M writes a day QPS/TPS = 200M/ (24 * 60 * 60)  = 2300 TPS
  - Read - 200M reads a day QPS - 200M/ (24 * 60 * 60) = 2300 QPS
  - Read to write - 1:1
- Storage
  - 3 years * 12 * 200M * 30 = 216 B
  - 216B * 10000 Bytes  = 21.6 TB
- Cache Memory
  - 23K * 500Bytes * 60 * 24 * 0.2(cache factor) = 186 GB
- Server
  - Number of operations per second 1000/t. t -> cpu work time in single thread
  - Concurrent threads in a server 100-200
  - Considering 100 threads 100*1000/t
  - Server considering 30-40%  0.3 * 100 * 1000/t
  - considering for read/write 10KB -> 200ms
  - 0.3 * 100 * 1000/200 = 150 RPS per server
  - 2300 + 2300 / 150 = 4600/150 = 30 Servers

- API Parallelization
  - NA
- Hotspots
  - Yes
- Availability & Geo distribution
  - Yes Geo distribution is required.

# System Overview

- Metadata Service
- FileStorage/Download Service
- Notification Service
- Comment Service
- Authentication Service

# Deep Dive Design  

![systemview](/blob/images/googledrive.png)

# API

  


# DB Schema
- uploadFile() type file resumable
- download()
  - path (download path file)
- fileRevision()
  - path
  - limit


# Reliability/ Fault tolerance / Scaling / Performance / Security

## Scalability

## Data Partition

## Data Replication

## Details
A candidate interviewing for SSE @ Google was asked to break down the design of Google Drive.

Another candidate who was interviewing for the role of SDE-III @ Amazon, was asked another with a file upload system question.

I’ve faced these too. System design rounds love “simple” file upload questions until you add one layer of complexity:

– Add virus scanning? Whole new security headache.
–  Add multi-region storage? Now you’re fighting replication and consistency.
–  Add instant previews or image compression? Welcome to async pipelines and job queues.

Here’s my personal checklist of 15 things you must get right when building file upload systems:

1. Never upload directly to your backend
→ Use presigned URLs so files go straight to S3, GCS, or your object storage, offloading bandwidth and freeing up backend resources.

2. Validate file type by content, not extension
→ Don't trust “.jpg” or “.pdf”, read the file’s magic bytes or headers to catch disguised executables or corrupted files.

3. Set strict file size limits (early)
→ Prevent memory blowups, denial of service, and accidental 50GB “cat video” uploads.

4. Multipart/chunked uploads for large files
→ Upload big files in chunks, so you can retry failed pieces, resume partial uploads, and never lose user progress.

5. Resumable uploads matter
→ User’s WiFi dies? Don’t make them start from scratch. Store upload progress, support resume tokens.

6. Async virus scanning before “marking ready”
→ Queue the scan; don’t let user-access or public-sharing happen until the result is clean.

7. Never trust user-supplied metadata
→ Recompute MIME types, image dimensions, video duration, etc., server-side, attackers will fake everything.

8. Expire unused presigned URLs fast
→ Every upload/download link should expire in minutes, not days. Stops replay attacks and stale-link leaks.

9. Background post-processing
→ Thumbnails, transcoding, compression, indexing, all should be async jobs, not blocking the upload.

10. Signed download URLs only
 → Never expose raw S3 or GCS paths. Every download link should be time-bound and permission-checked.

11. Enforce per-user and per-IP rate limits
→ Throttle abusive clients, prevent brute force, and stop sudden spikes from melting your backend.

12. Encrypt files at rest (and in transit)
 → Use server-side encryption (SSE) on S3 or GCS, plus HTTPS/TLS for every file transfer.

13. Version every upload
→ Store new files with unique IDs or version suffixes, never overwrite by default. Enables “undo” and rollback, and prevents race conditions.

14. Log every upload and access
→ Audit logs for every file action: who uploaded, who accessed, when, and from where. Critical for debugging and compliance.

15. Handle storage failures and edge cases gracefully
→ What happens if S3 times out? What if storage quota is exceeded? Handle partial failures, show clear errors, and keep users in the loop
