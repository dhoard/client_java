# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-07T05:06:29Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.04K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.22K | ± 175.87 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.79K | ± 839.66 | ops/s | 1.3x slower |
| prometheusAdd | 48.30K | ± 3.58K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 41.46 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.62K | ± 119.34 | ops/s | 10.0x slower |
| simpleclientAdd | 6.43K | ± 179.06 | ops/s | 10x slower |
| openTelemetryInc | 1.40K | ± 219.47 | ops/s | 47x slower |
| openTelemetryAdd | 1.40K | ± 144.71 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.23K | ± 12.35 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.31K | ± 2.04K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 34.22 | ops/s | 1.4x slower |
| prometheusNative | 3.01K | ± 299.67 | ops/s | 2.1x slower |
| openTelemetryClassic | 689.60 | ± 24.53 | ops/s | 9.2x slower |
| openTelemetryExponential | 554.63 | ± 20.20 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 481.96K | ± 4.09K | ops/s | **fastest** |
| prometheusWriteToNull | 477.15K | ± 6.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 469.50K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 459.15K | ± 2.27K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49787.637    ± 839.660  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1401.199    ± 144.706  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1404.773    ± 219.473  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1234.372     ± 12.353  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48303.285   ± 3575.379  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66040.323   ± 1005.640  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57222.090    ± 175.870  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6425.609    ± 179.065  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6773.208     ± 41.464  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6623.098    ± 119.338  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.599     ± 24.534  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.630     ± 20.201  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6314.280   ± 2040.137  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3014.465    ± 299.674  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.936     ± 34.215  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459153.425   ± 2269.865  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469496.567   ± 4731.156  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481957.093   ± 4093.495  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     477150.520   ± 6703.740  ops/s
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
