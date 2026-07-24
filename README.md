# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-24T06:23:32Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.03K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.86K | ± 1.10K | ops/s | 1.2x slower |
| prometheusAdd | 51.46K | ± 234.53 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.95K | ± 1.12K | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 227.69 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 23.97 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 359.40 | ops/s | 10x slower |
| openTelemetryAdd | 3.44K | ± 313.66 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.26K | ± 121.30 | ops/s | 20x slower |
| openTelemetryInc | 3.08K | ± 34.90 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.58K | ± 38.72 | ops/s | **fastest** |
| prometheusClassic | 5.21K | ± 1.64K | ops/s | 2.4x slower |
| prometheusClassicSingleThread | 4.59K | ± 13.44 | ops/s | 2.7x slower |
| simpleclient | 4.47K | ± 60.18 | ops/s | 2.8x slower |
| prometheusNative | 2.83K | ± 287.01 | ops/s | 4.4x slower |
| openTelemetryClassic | 774.17 | ± 18.42 | ops/s | 16x slower |
| openTelemetryExponential | 770.50 | ± 70.04 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.56K | ± 317.93 | ops/s | **fastest** |
| openMetricsWriteToNull | 22.90K | ± 806.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 503.65K | ± 3.83K | ops/s | **fastest** |
| prometheusWriteToByteArray | 498.80K | ± 4.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.11K | ± 2.03K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 476.40K | ± 4.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47950.212   ± 1122.124  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3443.242    ± 313.660  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3076.523     ± 34.902  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3262.614    ± 121.298  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51455.312    ± 234.530  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65033.476   ± 1096.015  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55863.237   ± 1099.824  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6248.927    ± 359.405  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6541.086    ± 227.687  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6376.962     ± 23.970  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        774.174     ± 18.418  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        770.502     ± 70.036  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5206.783   ± 1642.267  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12577.473     ± 38.724  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4594.741     ± 13.436  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2828.005    ± 287.008  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4465.338     ± 60.184  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22901.218    ± 806.641  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23558.511    ± 317.928  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476401.088   ± 4040.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478114.685   ± 2032.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498803.286   ± 4223.954  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503654.643   ± 3833.988  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
