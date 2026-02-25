# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-25T05:25:12Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.43K | ± 1.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.07K | ± 272.99 | ops/s | 1.1x slower |
| prometheusAdd | 50.91K | ± 672.65 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.72K | ± 961.23 | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 13.17 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.61K | ± 136.86 | ops/s | 9.7x slower |
| simpleclientAdd | 6.24K | ± 253.16 | ops/s | 10x slower |
| openTelemetryAdd | 1.25K | ± 92.49 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 69.09 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.20K | ± 42.82 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 414.68 | ops/s | **fastest** |
| simpleclient | 4.58K | ± 24.03 | ops/s | 1.1x slower |
| prometheusNative | 2.89K | ± 292.65 | ops/s | 1.8x slower |
| openTelemetryClassic | 710.63 | ± 35.07 | ops/s | 7.3x slower |
| openTelemetryExponential | 563.66 | ± 32.57 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.02K | ± 5.31K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.84K | ± 5.40K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.56K | ± 1.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.06K | ± 5.48K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49720.853    ± 961.230  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1246.297     ± 92.491  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.761     ± 69.094  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1203.176     ± 42.820  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50913.137    ± 672.649  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64428.493   ± 1284.455  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57068.514    ± 272.993  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6243.069    ± 253.156  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6764.711     ± 13.169  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6612.376    ± 136.860  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        710.634     ± 35.074  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.663     ± 32.566  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5198.866    ± 414.684  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2886.074    ± 292.646  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4583.995     ± 24.030  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482059.547   ± 5478.615  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488555.495   ± 1255.541  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488836.293   ± 5403.783  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495024.093   ± 5312.418  ops/s
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
