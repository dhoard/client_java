# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-11T07:49:24Z
- **Commit:** [`65d57b0`](https://github.com/dhoard/client_java/commit/65d57b020c6893283d5b4b85d76d86dfd7389cc8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 582.26 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 153.28 | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 571.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.12K | ± 284.82 | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 39.94 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 55.07 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 7.35 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.56K | ± 499.22 | ops/s | 19x slower |
| openTelemetryInc | 3.27K | ± 561.98 | ops/s | 20x slower |
| openTelemetryAdd | 2.88K | ± 39.60 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.05K | ± 1.57K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 76.65 | ops/s | 1.1x slower |
| prometheusNative | 2.88K | ± 391.71 | ops/s | 1.8x slower |
| openTelemetryClassic | 776.08 | ± 18.19 | ops/s | 6.5x slower |
| openTelemetryExponential | 636.14 | ± 77.13 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.82K | ± 358.97 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.81K | ± 66.76 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 506.52K | ± 5.64K | ops/s | **fastest** |
| prometheusWriteToByteArray | 501.73K | ± 5.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.14K | ± 6.83K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 479.75K | ± 3.19K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50121.281    ± 284.820  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2875.588     ± 39.600  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3270.300    ± 561.985  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3555.702    ± 499.217  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51270.010    ± 571.246  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66424.936    ± 582.259  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57002.096    ± 153.277  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6482.466     ± 55.066  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6531.220     ± 39.945  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6338.148      ± 7.348  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        776.085     ± 18.188  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        636.139     ± 77.127  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5053.409   ± 1568.130  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2882.266    ± 391.713  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.486     ± 76.651  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23810.379     ± 66.758  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23817.441    ± 358.975  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479746.778   ± 3189.347  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480137.424   ± 6834.741  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     501731.719   ± 5557.467  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506524.255   ± 5644.584  ops/s
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
