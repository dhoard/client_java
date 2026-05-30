# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-30T06:57:04Z
- **Commit:** [`f0a3b2e`](https://github.com/dhoard/client_java/commit/f0a3b2e46296428952756c95c9037982e7e9baa7)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.02K | ± 306.11 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.04K | ± 164.59 | ops/s | 1.2x slower |
| prometheusAdd | 49.92K | ± 1.57K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.43K | ± 8.28K | ops/s | 1.5x slower |
| simpleclientInc | 6.56K | ± 36.83 | ops/s | 10x slower |
| simpleclientAdd | 6.51K | ± 38.50 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 131.05 | ops/s | 10x slower |
| openTelemetryInc | 3.46K | ± 363.12 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.42K | ± 630.55 | ops/s | 19x slower |
| openTelemetryAdd | 2.99K | ± 72.85 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 1.84K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 68.73 | ops/s | 1.4x slower |
| prometheusNative | 2.96K | ± 301.36 | ops/s | 2.1x slower |
| openTelemetryClassic | 809.51 | ± 42.76 | ops/s | 7.6x slower |
| openTelemetryExponential | 637.42 | ± 74.96 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.57K | ± 975.78 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.56K | ± 194.52 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.76K | ± 6.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.70K | ± 4.19K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.58K | ± 5.49K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.78K | ± 1.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44431.616   ± 8277.483  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2991.581     ± 72.846  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3457.548    ± 363.120  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3416.747    ± 630.551  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49923.466   ± 1568.078  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66015.503    ± 306.106  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57040.408    ± 164.588  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6514.476     ± 38.502  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.340     ± 36.831  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6428.503    ± 131.046  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        809.508     ± 42.765  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        637.424     ± 74.958  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6185.447   ± 1838.808  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2955.516    ± 301.363  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.069     ± 68.726  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23562.209    ± 194.525  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23573.801    ± 975.778  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475778.556   ± 1851.048  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482579.918   ± 5487.589  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499696.050   ± 4188.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504760.940   ± 6133.377  ops/s
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
