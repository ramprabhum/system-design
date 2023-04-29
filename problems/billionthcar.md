# Functional Requirement

- Identify the billionth car which is streamed
- Failed messages from clients will be retried in an interval


# Non-Functional Requirement

- Consume data from different data sources
- Realtime update of the events


# System View

- EventConsumption Service
- EventAnalytics (MapReduce) - Batch
- Reprocess ony the impacted retries

![system view](/blob/images/billionthcar.png)

# API

- EventConsumption Service - Consumes events from clients
  - consumeEvent(car id, timestamp, bridge id)
- MapReduce 
  - sum(carid) > 1B sort by timestamp 


# Database Schema

- Event table
  - id (Primary Key)
  - car id
  - bridge id
  - timestamp
