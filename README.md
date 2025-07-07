# Alert_system-Pipeline

🔁  Alert Pipeline: End-to-End Flow

     ┌────────────┐
     │   Client   │ ← You (sending test alerts)
     └─────┬──────┘
           │
           ▼
 ┌─────────────────────┐
 │  Kafka Producer CLI │
 │ (e.g. kafka-console │
 │   -producer.sh)     │
 └────────┬────────────┘
          │ sends alert (JSON)
          ▼
 ┌────────────────────────────┐
 │     Kafka Broker (9092)    │
 │  Topic: alerts             │
 │  Handles message queueing  │
 └────────┬───────────────────┘
          │ consumes topic
          ▼
 ┌────────────────────────────┐
 │     alert_worker           │
 │ (Node.js Kafka Consumer)   │
 │  - Connects to Kafka       │
 │  - Listens to 'alerts'     │
 │  - Parses JSON             │
 │  - Inserts into PostgreSQL │
 └────────┬───────────────────┘
          │
          ▼
 ┌───────────────────────┐
 │  PostgreSQL Database  │
 │  Table: alerts        │
 │  Stores alert rows    │
 └───────────────────────┘
