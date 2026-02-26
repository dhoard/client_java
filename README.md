# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-26T05:21:50Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.16K | ± 393.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.28K | ± 147.19 | ops/s | 1.2x slower |
| prometheusAdd | 51.35K | ± 263.61 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.28K | ± 1.49K | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 40.48 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.45K | ± 200.81 | ops/s | 10x slower |
| simpleclientAdd | 6.41K | ± 147.40 | ops/s | 10x slower |
| openTelemetryAdd | 1.50K | ± 312.19 | ops/s | 44x slower |
| openTelemetryInc | 1.25K | ± 49.70 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.24K | ± 29.86 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.70K | ± 1.98K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 51.63 | ops/s | 1.5x slower |
| prometheusNative | 3.08K | ± 236.71 | ops/s | 2.2x slower |
| openTelemetryClassic | 677.80 | ± 52.89 | ops/s | 9.9x slower |
| openTelemetryExponential | 568.90 | ± 22.62 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 484.80K | ± 2.26K | ops/s | **fastest** |
| prometheusWriteToNull | 480.20K | ± 8.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.54K | ± 4.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 457.30K | ± 11.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48284.241   ± 1488.664  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1499.317    ± 312.191  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.841     ± 49.700  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1240.068     ± 29.862  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51349.784    ± 263.614  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66162.585    ± 393.475  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57275.254    ± 147.194  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6405.628    ± 147.401  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6764.125     ± 40.477  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6445.483    ± 200.807  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.799     ± 52.886  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.898     ± 22.617  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6701.224   ± 1981.115  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3076.192    ± 236.706  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.321     ± 51.634  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473536.529   ± 4904.750  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     457300.345  ± 11290.957  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484802.746   ± 2259.306  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     480201.922   ± 8851.621  ops/s
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
