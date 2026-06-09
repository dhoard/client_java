# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-09T07:16:10Z
- **Commit:** [`65d57b0`](https://github.com/dhoard/client_java/commit/65d57b020c6893283d5b4b85d76d86dfd7389cc8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.35K | ± 2.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.94K | ± 578.20 | ops/s | 1.1x slower |
| prometheusAdd | 48.61K | ± 892.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.36K | ± 230.73 | ops/s | 1.3x slower |
| simpleclientInc | 6.19K | ± 83.93 | ops/s | 9.4x slower |
| simpleclientAdd | 6.12K | ± 59.88 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.92K | ± 20.02 | ops/s | 9.8x slower |
| openTelemetryInc | 4.84K | ± 895.21 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.81K | ± 1.04K | ops/s | 12x slower |
| openTelemetryAdd | 3.43K | ± 146.59 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 1.64K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 51.55 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 252.63 | ops/s | 1.8x slower |
| openTelemetryClassic | 766.08 | ± 8.42 | ops/s | 7.1x slower |
| openTelemetryExponential | 567.09 | ± 35.39 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.23K | ± 561.15 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.55K | ± 593.77 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 575.36K | ± 16.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.70K | ± 4.71K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 545.09K | ± 5.26K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 535.15K | ± 3.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44357.120    ± 230.732  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3425.514    ± 146.590  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4835.815    ± 895.209  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4814.107   ± 1037.650  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48612.620    ± 892.063  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58345.449   ± 2530.171  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50939.663    ± 578.204  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6117.919     ± 59.876  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6188.031     ± 83.928  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5924.608     ± 20.016  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        766.079      ± 8.423  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.087     ± 35.395  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5473.696   ± 1640.118  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3009.097    ± 252.634  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4485.141     ± 51.551  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26548.110    ± 593.773  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27232.121    ± 561.153  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535154.255   ± 3732.028  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     545089.087   ± 5256.864  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568699.564   ± 4709.615  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     575356.558  ± 16819.178  ops/s
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
