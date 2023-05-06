# Functional Requirements
- Direct & group messaging between users (Write/Delete)
  - Texts
  - Pictures/Videos
- User Registration
- Message Status
  - Send All/Individual
  - Recieved All/Individual
  - Read All/Individual
- User Status

# Non Functional Requirements
- Highly consistent and available systems 
- Faster reads 
- Should be able to scale up for large requests

# Design Considerations
- Highly available system
- Consistent systems
- MAU = 2 Billion
- DAU = 25 million
- Messages per day 4000 * 25 = 100 Billion messages
- Groups can have max 200 members, 16MB max size, max message size 700, 10% pictures & videos
- DB read = 10ms , Cache Read = 2ms, App = 1ms

# System Overview

- Messaging Service (Text,Blobs(stores/sends pics videos))
- Discovery Service
- Group Service
- Profile Services
- Notification Services

# Deep Dive Design

![systemview](/blob/images/messagingsystem.png)

# API
- Messaging Service
  - createConversation(message, recipient, group, blob)
  - sendMessages(userId)
  - updateConversationId(conversationId)
- Group Service
  - fanOut(groupId,messageId)
- Profile Service
  - getProfile(userID)
  - createUser(name,picture)
- Discovery Service
  - updateServer(userId, serverId)
  - updateLastSeen(userId)




# DB Schema
- Conversation
  - id
  - messageId
  - userId
  - groupId
  - createdAt
  - status
- Message
  - id
  - author
  - message
  - blobURL
- Group
  - id
  - groupId
  - userId
- Profile
  - id
  - name
  - pictureUrL
- Discovery
  - id
  - profileId
  - server
  - lastSeen


# Reliability/ Fault tolerance / Scaling / Performance / Security

## Scalability

## Data Partition

## Data Replication


# Capacity Estimation

- Profile Service
  - Storage
    - id 8bytes
    - name 200 bytes
    - pictureUrL 100 bytes
    - Total - 308 bytes
    - 2 Billion users * 308  = 616 GB
  - Server (Cahce Reads)
    - Number of operations per second 1000/t. t -> cpu work time in single thread
    - Concurrent threads in a server 100-200
    - Considering 100 threads 100*1000/t
    - Server considering 30-40%  0.3 * 100 * 1000/t
    - considering for read/write 1million QPS -> 2ms (Cache)
    - 0.2 * 100 * 1000/2 = 10000 RPS per server
    - 1 Million / 10000 = 100 Servers
- Messaging Service
  - Storage(Messaging)
    - id 8bytes
    - author 8 bytes
    - message  700 bytes
    - blobUrL 100 bytes
    - Total - 800 bytes
    - 100 Billion message * 800 bytes * 1500 days  = 1.2 exabytes
    - ( SSD - 100 TB => 10000 SSD(100TB) = 1 EXB * 3(replication)  = 30000 SSD => 7500 machines(4 SSD per machine)
  - Server (Cahce Reads)
    - 2 Billion MAU
    - 65000 Sockets connection in a machine (asuume 50000)
    - Commodity machine will have 100 threads (50%) => 50 threads per machine
    - 1 thread - 1000 web sockets  =>  each machine will have 50000 WS
    -  2 billion/ 50000 = 40K machines

- API Parallelization
  - NA
- Hotspots
  - Yes
- Availability & Geo distribution
  - Yes Geo distribution is required.