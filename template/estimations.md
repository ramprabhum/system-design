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
