# Ride Sharing Real-Time Analytics with Apache Spark

## Project Structure

This project demonstrates real-time streaming and analytics using Apache Spark Structured Streaming. It consists of a data generator and three Spark tasks.

---

## 📊 Dataset Description

The streaming data represents ride-sharing trip events, generated in real-time via a socket server. Each record is in JSON format:

| Field        | Type     | Description                              |
|--------------|----------|------------------------------------------|
| trip_id      | String   | Unique identifier for each trip          |
| driver_id    | Integer  | ID of the driver                         |
| distance_km  | Float    | Distance of the ride in kilometers       |
| fare_amount  | Float    | Fare charged for the trip                |
| timestamp    | String   | Event time in `YYYY-MM-DD HH:MM:SS` format |

---

## 🔄 Data Generation

**File**: `data_generator.py`

This Python script simulates ride-sharing data and sends it via a TCP socket to `localhost:9999`.

### How to run:

```bash
python data_generator.py
```

This starts a streaming server that sends one JSON ride event per second.

---

## Task 1: Basic Structured Streaming to CSV

**File**: `task1.py`

### Features:
- Reads streaming data from socket
- Parses JSON and converts to structured columns
- Stores output as CSV files to `output/streaming_data/`

### Run:

```bash
spark-submit task1.py
```

---

## Task 2: Micro-Batch Processing with foreachBatch

**File**: `task2.py`

### Features:
- Uses `foreachBatch` to process and save each micro-batch
- Appends data to batch-specific CSV files under `output/aggregated/`

### Run:

```bash
spark-submit task2.py
```

---

##  Task 3: Time Window Aggregation

**File**: `task3.py`

### Features:
- Parses and casts timestamps
- Adds watermark to handle late data
- Aggregates total fare over 5-minute windows
- Saves windowed results per batch to `output/window/`

### Run:

```bash
spark-submit task3.py
```

---


## Directory Layout

```
.
├── data_generator.py
├── task1.py
├── task2.py
├── task3.py
├── output/
│   ├── streaming_data/
│   ├── aggregated/
│   └── window/
```

---

## ✅ Requirements

- Python 3.x
- Apache Spark 3.x
- Java 8+
- PySpark
- Faker (`pip install faker`)

