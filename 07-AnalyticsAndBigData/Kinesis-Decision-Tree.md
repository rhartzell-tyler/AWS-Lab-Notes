# ⚡ Kinesis Decision Tree  
### *“If the question says X → choose Y”*

---

# 1. Start With: Do you need REAL‑TIME PROCESSING?

```
IF the question says:
    "real-time analytics"
    "SQL on streaming data"
    "windowed aggregations"
    "joins"
    "stateful processing"
    "detect anomalies"
    "continuous queries"
THEN → Kinesis Data Analytics (KDA)
```

**Why:**  
KDA is the ONLY Kinesis service that performs **actual processing**.

---

# 2. Do you need CUSTOM PROCESSING or MULTIPLE CONSUMERS?

```
IF the question says:
    "multiple consumers"
    "Lambda consumers"
    "custom processing logic"
    "ordering per shard"
    "enhanced fan-out"
    "replay / reprocess data"
    "retention > 24 hours"
THEN → Kinesis Data Streams (KDS)
```

**Why:**  
KDS is the real streaming engine with shards, consumers, ordering, and replay.

---

# 3. Do you need SIMPLE INGESTION + DELIVERY?

```
IF the question says:
    "ingest and deliver"
    "load into S3/Redshift/OpenSearch"
    "minimal transformation"
    "convert to Parquet/ORC"
    "buffer then deliver"
    "fully managed"
    "no consumers"
THEN → Kinesis Data Firehose (KDF)
```

**Why:**  
Firehose is ingestion + buffering + delivery.  
It is NOT a processing engine.

---

# 4. Do you need LIGHTWEIGHT TRANSFORMATION ONLY?

```
IF the question says:
    "mask fields"
    "add metadata"
    "convert JSON to Parquet"
    "simple record transformation"
THEN → Kinesis Data Firehose (KDF) with Lambda transform
```

**Why:**  
Firehose supports only **light** per-record transforms.

---

# 5. Do you need to REPLAY or REPROCESS data?

```
IF the question says:
    "replay"
    "reprocess"
    "long retention"
    "audit or re-run consumers"
THEN → Kinesis Data Streams (KDS)
```

**Why:**  
Firehose cannot replay.  
KDA cannot replay.  
Only **Streams** can.

---

# 6. Do you need EXACT ORDERING?

```
IF the question says:
    "ordering"
    "partition key"
    "shard-level ordering"
THEN → Kinesis Data Streams (KDS)
```

**Why:**  
Firehose has no ordering.  
KDA inherits ordering from Streams.

---

# 7. Do you need the EASIEST possible ingestion?

```
IF the question says:
    "fully managed"
    "no administration"
    "no shards"
    "no scaling"
    "just deliver the data"
THEN → Kinesis Data Firehose (KDF)
```

**Why:**  
Firehose is the simplest ingestion path.

---

# 8. Summary Table (Quick Reference)

| Requirement | Choose |
|------------|--------|
| Real-time SQL / analytics | **Kinesis Data Analytics** |
| Custom processing / multiple consumers | **Kinesis Data Streams** |
| Ingest → buffer → deliver | **Kinesis Data Firehose** |
| Replay / reprocess | **Kinesis Data Streams** |
| Ordering | **Kinesis Data Streams** |
| Convert to Parquet/ORC | **Kinesis Data Firehose** |
| Simple ingestion | **Kinesis Data Firehose** |
| Stateful or windowed processing | **Kinesis Data Analytics** |

---

# 9. One-Sentence Mental Models

**Kinesis Data Streams** = real-time streaming engine (shards, consumers, replay).  
**Kinesis Data Firehose** = ingestion + buffering + delivery + light transforms.  
**Kinesis Data Analytics** = real-time SQL/processing on top of Streams or Firehose.


---

The correct mental model going forward
Here’s the rule that will prevent this mistake forever:

🔒 If the question says “transform” but NOT “analytics,” assume Firehose.

If the question says:
- “SQL”
- “real‑time analytics”
- “windowed
- “stateful”
- “joins”

→ **Kinesis Data Analytics**

If the question says:
- “ingest and transform”
- “convert to Parquet”
- “mask fields”
- “simple transformation”
- “deliver to S3”

→ **Kinesis Data Firehose**

If the question says:
- “multiple consumers”
- “replay”
- “ordering”
- “custom processing”

→ **Kinesis Data Streams**