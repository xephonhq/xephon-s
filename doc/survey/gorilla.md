# Gorilla (Beringei)

- https://github.com/facebookincubator/beringei

## TODO

- [ ] does gorilla use milliseconds?
- [ ] `PutDataRequest` seems low efficient, why not use list on `TimeValuePair`, though with zlib, the impact of duplication of key could be reduced a lot

## Meta

- Time interval: varies
- Time precision: Unix timestamp in milliseconds? (64bit)
  - 1491502273                    (second)
  - 1491502273000                 (millisecond)
  - 1491502273000000              (microsecond)
  - 1491502273000000000           (nanosecond)
  - 2147483647                    (max of int32 is not enough for millisecond, unit32 won't help)
  - 9223372036854775807           
- Value precision: 64 bit float
- Store Timestamp: Yes
- Time and value are compressed separately

## Compression

- The paper has error https://github.com/facebookincubator/beringei/issues/17

[beringei_data.thrift](https://github.com/facebookincubator/beringei/blob/master/beringei/if/beringei_data.thrift)

````
struct TimeValuePair {
  1: i64 unixTime,
  2: double value,
}

struct DataPoint {
  1: Key key,
  2: TimeValuePair value,
  3: i32 categoryId,
}

struct PutDataRequest {
  1: list<DataPoint> data,
}

struct PutDataResult {
  // return not owned data points
  1: list<DataPoint> data,
}
````

## Architecture

### On Disk

- Section 4.3 in paper

#### Log

**only one append-only log per shard, so values within a shard are interleaved across time series**

- use 32-bit int to identify Time Value pair in log (thus **much larger** than in memory blocks)
- not WAL, use large buffer to increase performance
- [ ] TODO: link to code
- [ ] TODO: compressed block, each series has own block?
