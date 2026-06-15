# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-15T08:23:36Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.90K | ± 1.76K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.62K | ± 361.76 | ops/s | 1.1x slower |
| prometheusAdd | 51.20K | ± 325.08 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.33K | ± 1.94K | ops/s | 1.3x slower |
| simpleclientInc | 6.66K | ± 108.77 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.38K | ± 43.66 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 173.69 | ops/s | 10x slower |
| openTelemetryAdd | 3.27K | ± 304.35 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.17K | ± 239.49 | ops/s | 20x slower |
| openTelemetryInc | 3.07K | ± 214.17 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.20K | ± 1.24K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 43.47 | ops/s | 1.2x slower |
| prometheusNative | 2.70K | ± 386.90 | ops/s | 1.9x slower |
| openTelemetryClassic | 753.91 | ± 53.83 | ops/s | 6.9x slower |
| openTelemetryExponential | 580.18 | ± 41.69 | ops/s | 9.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.05K | ± 406.05 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.23K | ± 163.71 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.03K | ± 3.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.64K | ± 5.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.16K | ± 2.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.67K | ± 4.99K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49330.466   ± 1938.133  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3272.365    ± 304.350  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3073.743    ± 214.167  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3168.650    ± 239.491  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51199.396    ± 325.084  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63902.502   ± 1758.162  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56623.289    ± 361.762  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6323.898    ± 173.689  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6655.692    ± 108.767  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6375.991     ± 43.660  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        753.914     ± 53.831  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.175     ± 41.690  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5201.421   ± 1243.622  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2702.741    ± 386.903  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4389.009     ± 43.470  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23225.489    ± 163.715  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24046.786    ± 406.046  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475674.809   ± 4990.924  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481155.834   ± 2639.787  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494637.224   ± 5824.891  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502031.160   ± 3979.281  ops/s
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
