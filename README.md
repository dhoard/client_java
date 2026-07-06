# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-06T07:33:30Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.52K | ± 2.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.51K | ± 79.79 | ops/s | 1.1x slower |
| prometheusAdd | 51.41K | ± 196.57 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.79K | ± 1.05K | ops/s | 1.3x slower |
| simpleclientInc | 6.62K | ± 124.97 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.36K | ± 25.96 | ops/s | 10.0x slower |
| simpleclientAdd | 6.15K | ± 241.54 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.35K | ± 377.75 | ops/s | 19x slower |
| openTelemetryAdd | 3.30K | ± 374.91 | ops/s | 19x slower |
| openTelemetryInc | 3.13K | ± 142.56 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 55.67 | ops/s | **fastest** |
| prometheusClassic | 4.38K | ± 569.13 | ops/s | 1.0x slower |
| prometheusNative | 2.59K | ± 90.08 | ops/s | 1.7x slower |
| openTelemetryClassic | 779.33 | ± 30.34 | ops/s | 5.7x slower |
| openTelemetryExponential | 623.65 | ± 64.29 | ops/s | 7.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.09K | ± 668.71 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.26K | ± 58.26 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 510.11K | ± 3.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.28K | ± 4.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.94K | ± 6.19K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 482.26K | ± 2.64K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49792.132   ± 1053.891  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3295.064    ± 374.915  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3133.625    ± 142.558  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3346.187    ± 377.748  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51407.706    ± 196.567  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63521.261   ± 2530.456  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56513.783     ± 79.792  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6147.913    ± 241.539  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6619.526    ± 124.974  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.049     ± 25.957  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        779.331     ± 30.336  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        623.646     ± 64.287  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4380.508    ± 569.135  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2591.706     ± 90.079  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.346     ± 55.670  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23255.602     ± 58.264  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24087.657    ± 668.712  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482262.265   ± 2639.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482940.410   ± 6190.125  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493284.630   ± 4121.960  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     510113.139   ± 3948.534  ops/s
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
