# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-12T06:46:54Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.60K | ± 494.77 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.12K | ± 518.40 | ops/s | 1.1x slower |
| prometheusAdd | 48.83K | ± 876.20 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.85K | ± 1.70K | ops/s | 1.4x slower |
| simpleclientInc | 6.20K | ± 5.71 | ops/s | 9.6x slower |
| simpleclientAdd | 6.08K | ± 34.36 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.84K | ± 57.09 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.26K | ± 1.29K | ops/s | 11x slower |
| openTelemetryInc | 4.42K | ± 923.95 | ops/s | 13x slower |
| openTelemetryAdd | 3.30K | ± 166.62 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 1.69K | ops/s | **fastest** |
| simpleclient | 4.05K | ± 152.41 | ops/s | 1.2x slower |
| prometheusNative | 2.92K | ± 242.00 | ops/s | 1.7x slower |
| openTelemetryClassic | 716.18 | ± 23.15 | ops/s | 7.0x slower |
| openTelemetryExponential | 549.59 | ± 13.41 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.28K | ± 380.47 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.02K | ± 285.91 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 584.60K | ± 4.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 574.87K | ± 5.14K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.90K | ± 7.75K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 533.66K | ± 3.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42849.163   ± 1701.060  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3301.645    ± 166.624  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4416.504    ± 923.954  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5255.897   ± 1288.516  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48831.289    ± 876.201  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59600.817    ± 494.772  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52118.025    ± 518.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6083.855     ± 34.364  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6200.658      ± 5.708  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5840.030     ± 57.095  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        716.182     ± 23.146  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.592     ± 13.406  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5026.413   ± 1693.275  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2924.033    ± 242.002  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4051.842    ± 152.409  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27021.124    ± 285.907  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27279.031    ± 380.474  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     533660.798   ± 3280.597  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546904.174   ± 7747.434  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     574867.345   ± 5137.202  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     584598.866   ± 4746.145  ops/s
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
