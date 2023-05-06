# Capacity Estimation

- Traffic  - 20M Writes per day - 2B Reads per day
    - Write - 20M writes a day QPS/TPS = 20M/ (24 * 60 * 60)  = 230 TPS
    - Read - 2B reads a day QPS - 2B/ (24 * 60 * 60) = 23K QPS
    - Read to write - 100:1
- Storage
    - 3 years * 12 * 20M * 30 = 21.6 B
    - 21.6B * 500Bytes  = 1.08 TB
- Cache Memory
    - 23K * 500Bytes * 60 * 24 * 0.2(cache factor) = 186 GB
- - Server
  - Number of operations per second 1000/t. t -> cpu work time in single thread
  - Concurrent threads in a server 100-200
  - Considering 100 threads 100*1000/t
  - Server considering 30-40%  0.3 * 100 * 1000/t

- API Parallelization
- Hotspots
- Availability & Geo distribution

# Reasons to scale
- Storage
  - a = number of rows
  - b = size of rows
  - c = TPS/QPS 
  - a * b / c* b * years in seconds / c* b * ttl in seconds
- Throughput
- high response time
- hih latency
- hotspots
- availability, geolocations

# Calculations Example

- DB read = 10ms , Cache Read = 2ms, App = 1ms
- Thread  = 1000/t ops
  - DB 1000/10 = 100 OPS
  - Cache 1000/2 = 500 OPS
  - App 1000/1 = 1000 OPS
