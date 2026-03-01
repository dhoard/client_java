# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-01T05:28:01Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.80K | ± 1.67K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 265.90 | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 188.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.60K | ± 2.04K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 168.32 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.49K | ± 151.13 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 30.40 | ops/s | 11x slower |
| openTelemetryInc | 1.52K | ± 185.66 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.36K | ± 221.89 | ops/s | 48x slower |
| openTelemetryAdd | 1.32K | ± 69.73 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 45.30 | ops/s | **fastest** |
| prometheusClassic | 4.17K | ± 124.43 | ops/s | 1.1x slower |
| prometheusNative | 3.01K | ± 243.10 | ops/s | 1.5x slower |
| openTelemetryClassic | 691.72 | ± 12.29 | ops/s | 6.5x slower |
| openTelemetryExponential | 541.39 | ± 10.71 | ops/s | 8.4x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.51K | ± 3.87K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.16K | ± 1.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.48K | ± 2.59K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.60K | ± 4.11K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49598.915   ± 2036.603  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1316.934     ± 69.732  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1523.700    ± 185.656  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1357.572    ± 221.894  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51600.183    ± 188.835  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65798.272   ± 1674.267  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56986.116    ± 265.895  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6071.026     ± 30.399  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6623.423    ± 168.323  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6487.441    ± 151.130  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.717     ± 12.294  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.389     ± 10.706  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4174.402    ± 124.430  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3005.962    ± 243.100  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4528.350     ± 45.302  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475595.383   ± 4109.227  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483484.498   ± 2588.932  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492158.808   ± 1949.503  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492506.750   ± 3867.332  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
