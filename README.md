# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-19T05:27:13Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.39K | ± 336.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.05K | ± 379.42 | ops/s | 1.1x slower |
| prometheusAdd | 51.36K | ± 325.65 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.88K | ± 1.14K | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 14.94 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.70K | ± 14.36 | ops/s | 9.8x slower |
| simpleclientAdd | 6.34K | ± 170.38 | ops/s | 10x slower |
| openTelemetryAdd | 1.60K | ± 203.57 | ops/s | 41x slower |
| openTelemetryIncNoLabels | 1.35K | ± 120.60 | ops/s | 48x slower |
| openTelemetryInc | 1.29K | ± 49.21 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.51K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 64.63 | ops/s | 1.2x slower |
| prometheusNative | 2.70K | ± 192.30 | ops/s | 2.0x slower |
| openTelemetryClassic | 706.68 | ± 44.19 | ops/s | 7.8x slower |
| openTelemetryExponential | 559.26 | ± 34.58 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.50K | ± 2.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.06K | ± 6.05K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 487.46K | ± 2.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.75K | ± 1.80K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48875.224   ± 1142.410  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1596.967    ± 203.565  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1292.879     ± 49.208  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1351.478    ± 120.605  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51358.183    ± 325.654  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65393.269    ± 336.689  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57049.409    ± 379.421  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6337.648    ± 170.385  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6762.943     ± 14.943  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6701.391     ± 14.365  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        706.679     ± 44.194  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.265     ± 34.585  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5511.212   ± 1625.990  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2703.326    ± 192.303  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4504.598     ± 64.635  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487462.391   ± 2300.230  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486745.419   ± 1803.939  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495061.269   ± 6048.797  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496500.612   ± 2277.134  ops/s
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
