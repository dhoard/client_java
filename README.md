# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-14T07:41:20Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.60K | ± 467.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.46K | ± 1.04K | ops/s | 1.2x slower |
| prometheusAdd | 48.23K | ± 528.80 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.19K | ± 1.21K | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 46.15 | ops/s | 9.7x slower |
| simpleclientAdd | 6.00K | ± 131.87 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.92K | ± 20.98 | ops/s | 10x slower |
| openTelemetryInc | 4.90K | ± 937.94 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.35K | ± 409.60 | ops/s | 14x slower |
| openTelemetryAdd | 4.10K | ± 797.65 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.25K | ± 453.42 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 72.66 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 139.31 | ops/s | 1.9x slower |
| openTelemetryClassic | 706.18 | ± 19.41 | ops/s | 7.4x slower |
| openTelemetryExponential | 548.38 | ± 7.60 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.72K | ± 252.02 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.39K | ± 146.42 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 583.82K | ± 9.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.23K | ± 3.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 544.70K | ± 4.99K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 529.53K | ± 10.81K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44187.149   ± 1209.000  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4103.048    ± 797.645  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4904.657    ± 937.941  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4348.634    ± 409.597  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48229.188    ± 528.797  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59601.486    ± 467.542  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51459.774   ± 1040.854  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5998.426    ± 131.867  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6153.659     ± 46.154  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5924.169     ± 20.980  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        706.176     ± 19.405  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.377      ± 7.599  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5245.033    ± 453.418  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2790.806    ± 139.306  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.975     ± 72.660  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27389.536    ± 146.417  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27724.517    ± 252.016  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529531.501  ± 10814.054  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     544701.190   ± 4993.705  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572232.027   ± 3913.362  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     583823.922   ± 9490.337  ops/s
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
