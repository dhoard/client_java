# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-22T07:14:03Z
- **Commit:** [`0bc0408`](https://github.com/dhoard/client_java/commit/0bc040814f37610ca3bb7b1f1474dbecdb20668d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.05K | ± 2.29K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.21K | ± 396.79 | ops/s | 1.1x slower |
| prometheusAdd | 48.92K | ± 1.15K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.05K | ± 317.46 | ops/s | 1.3x slower |
| simpleclientInc | 6.08K | ± 27.98 | ops/s | 9.6x slower |
| simpleclientAdd | 5.98K | ± 246.01 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.88K | ± 27.06 | ops/s | 9.9x slower |
| openTelemetryInc | 4.62K | ± 1.07K | ops/s | 13x slower |
| openTelemetryIncNoLabels | 4.45K | ± 338.01 | ops/s | 13x slower |
| openTelemetryAdd | 3.45K | ± 131.21 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.09K | ± 2.13K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 50.11 | ops/s | 1.3x slower |
| prometheusNative | 2.90K | ± 177.51 | ops/s | 2.1x slower |
| openTelemetryClassic | 712.84 | ± 24.36 | ops/s | 8.5x slower |
| openTelemetryExponential | 564.05 | ± 40.34 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.76K | ± 84.50 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.47K | ± 216.94 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.43K | ± 3.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 574.28K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.01K | ± 5.55K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 534.97K | ± 5.44K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44052.349    ± 317.458  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3446.473    ± 131.210  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4624.306   ± 1074.901  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4445.589    ± 338.009  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48918.298   ± 1146.142  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58054.547   ± 2291.564  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51211.217    ± 396.789  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5977.993    ± 246.006  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6076.643     ± 27.975  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5884.856     ± 27.060  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.839     ± 24.360  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        564.054     ± 40.340  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6094.118   ± 2130.180  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2898.237    ± 177.513  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4560.787     ± 50.114  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27467.309    ± 216.938  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27760.798     ± 84.496  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     534969.983   ± 5437.881  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546007.994   ± 5545.291  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     574279.825   ± 3061.415  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585429.245   ± 3641.819  ops/s
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
