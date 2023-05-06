# Functional Requirements
- Search Engine Indexing
- Web Archiving - collect & store data 
- Web Mining
- Web Crawling - ecommerce website crawling, copyright violations
  - crawl HTMLs
    - indexing
    - avoid duplicate
    - time limit of storage
    - frequency of crawls
  - Politness / RateLimiting
  - Honor robots.txt
  - Avoid spams, infinite loops & malicious content

# Non Functional Requirements
- Total page = 5 billion 
- OPS  = 5 Billion (monthly frequency)/ (30 days * 100000s) = 1666 => 2000 Ops
- Average page size = 100kb
- 
# Design Considerations
- Highly available system
- Intense compute systems

# System Overview
- Seed URL - start of crawl
- URL frontier - URLs to be downloaded
- HTML Downloader
- Content Parser
- Content Seen Service
- URL Extractor
- URL filter
- URL Seen Service


# Deep Dive Design

![systemview](/blob/images/webcrawler.png)

# API


# DB Schema



# Reliability/ Fault tolerance / Scaling / Performance / Security

## Scalability

## Data Partition

## Data Replication


# Capacity Estimation

- Storage (YES)
    - Total Pages = 5 billion pages
    -  5 Billion pages  * 100 kB * 12  months * 5 Years  =  30 PB
- Server (MAYBE) Bandwidth
    - 1 time crawling (5 Billion pages * 100KB ) = 0.5 PB
    - 10 GBps => 0.5PB/10GBps = 5days
    - 1000 servers can utilize 10GBps if every server is downloading 1 MBPS


- API Parallelization
    - YES
- Hotspots
    - NO
- Availability & Geo distribution
    - YES