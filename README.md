# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-29T07:20:21Z
- **Commit:** [`f0a3b2e`](https://github.com/dhoard/client_java/commit/f0a3b2e46296428952756c95c9037982e7e9baa7)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.11K | ± 1.75K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.40K | ± 805.65 | ops/s | 1.2x slower |
| prometheusAdd | 51.17K | ± 671.28 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.46K | ± 1.32K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 34.89 | ops/s | 9.9x slower |
| simpleclientAdd | 6.40K | ± 68.92 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 34.96 | ops/s | 10x slower |
| openTelemetryInc | 3.82K | ± 414.84 | ops/s | 17x slower |
| openTelemetryIncNoLabels | 3.50K | ± 712.13 | ops/s | 19x slower |
| openTelemetryAdd | 3.34K | ± 583.44 | ops/s | 19x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.52K | ± 1.25K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 61.97 | ops/s | 1.2x slower |
| prometheusNative | 2.98K | ± 335.46 | ops/s | 1.9x slower |
| openTelemetryClassic | 795.44 | ± 21.01 | ops/s | 6.9x slower |
| openTelemetryExponential | 653.03 | ± 90.80 | ops/s | 8.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.47K | ± 758.56 | ops/s | **fastest** |
| openMetricsWriteToNull | 24.36K | ± 98.06 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 495.58K | ± 6.13K | ops/s | **fastest** |
| prometheusWriteToNull | 495.00K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.65K | ± 5.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.09K | ± 4.74K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48459.235   ± 1322.156  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3340.601    ± 583.443  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3817.893    ± 414.839  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3498.934    ± 712.127  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51171.296    ± 671.279  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65105.609   ± 1747.528  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56398.777    ± 805.654  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6402.381     ± 68.919  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6553.861     ± 34.888  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6352.307     ± 34.963  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        795.437     ± 21.013  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        653.026     ± 90.802  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5515.110   ± 1246.089  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.130    ± 335.462  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4441.676     ± 61.973  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24361.653     ± 98.065  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24465.064    ± 758.557  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476089.764   ± 4737.772  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476647.999   ± 5113.673  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495584.576   ± 6131.499  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494996.137   ± 4629.325  ops/s
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
