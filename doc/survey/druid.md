# Druid


## Stories from the Trenches – The Challenges of Building an Analytics Stack

https://www.youtube.com/watch?v=Sz4w75xRrYM

![druid](druid.png)

- Immutable data
- In Memory is Overrated
  - mmap + SSD
  - cost of scaling CPU << cost of adding RAM
  - decompression on the fly (LZF, Snappy, LZ4)
- Low Latency vs High throughput
  - combine batch + streaming
  - immutable made it easy to combine the two ingestion methods
  - Makes for easy backfill and re-processing
  - Historical Node
  - Real-time Node
- Not All Data is Created Equal
  - user really care about recent data
  - user still want to run quarterly report
  - large queries create bottlenecks and resource contention
- Smarter Rebalancing
- Create Data Tiers
- Addressing Multitenancy
  - HyperLogLog sketches
  - Approximate top-k
  - Approximate histograms (monitoring)
- Monitoring
  - Use Druid to monitor Druid
- **Use cases should define engineering**

## Druid: A Real-time Analytical Data Store

- time series data with both numeric and text value
- a set dimension columns
  - KairosDB etc. are not multi dimension, strictly speaking
  - query over any arbitrary combination of dimensions

Features for a dashboard

- query latency
- multi-tenant
- HA
- make business decisions in "real-time"

### Architecture

> The name Druid comes from the Druid class in many role-playing games: it is a
shape-shifter, capable of taking on many different forms to fulfill
various different roles in a group.

- real time node
- historical node
- broker node
- coordinator node
