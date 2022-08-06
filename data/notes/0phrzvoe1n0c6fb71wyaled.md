## General Info

Makes it easy to collect, process and analyze realtime streaming data.

- Real time
- Fully managed
- Scalable
- Pay as you go

There are four types of service offerings:

1. Kinesis Data Streams
2. Kinesis Video Streams
3. Kinesis Data Firehouse
4. Kinesis Data Analytics

## Use Cases

- Log and Event Data Collection
- Real time analytics
- Mobile data capture
- Gaming data feed

## Key Concepts

**Shard**: base throughput unit of the stream.

- Append only log
- Ordered sequence of records
- Can ingest 1 MB/Sec
- More shards means more ingestion capacity

**Data Stream**:

- Logical grouping of shards no bound on number of shards
- Data is retained for retain data for 24hrs to 7 days

**Partition Key**:

- Meaningful identifier
- Used to route data records to different shards

**Sequence Number**:

- Unique Identifier for each data record assigned by Kinesis on record creation

**Data Record**:

- Unit of data stored
- Composed of a sequence number, partition key and data blob.
- Max size of the blob is 1 MB

**Data Producer**:

- Application that emits data records to the stream
- It assigns partition keys to records
- Partition keys determine which shard consumes the data

**Data Consumer**:

- Application or AWS Service that gets the data from the stream
