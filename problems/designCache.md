# Functional Requirements

- Get the value based on cache key
- Update/insert the value for a key
- Value can be a Json/String/XML


# Non Functional Requirements

- Must scale for more use cases
- Latency should be <10ms
- Highly available systems >99.96


# Design Considerations

- Eviction Policies (LRU LFU FIFO MRU)
- Access Patterns (Write through , Write around, Write back)
- Size based evictions/update policies
- Low latency & high availability


# System Overview

![systemview](/blob/images/cache.png)





# DeepDiveDesign

- Eventual consistent update recommended
- Leaderless update. Mcrouter maintains the details of the key distributed across machines



# API

- getDoc(List<String> key)
- putDoc(String key,Object value, DateTime TTL)


# DB Schema



# Reliability/ Fault tolerance / Scaling / Performance / Security
- Scale by adding more servers which can be horizontally & vertically scaled up
- Any failures data will not be backed up and data will be inconsistent and consistency not possible