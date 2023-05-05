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

# Design Considerations
- Highly consistent and available systems
- Faster reads
- Should be able to scale up for large requests

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
