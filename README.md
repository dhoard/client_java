# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-17T05:24:04Z
- **Commit:** [`8c229df`](https://github.com/dhoard/client_java/commit/8c229df26e7779246e88f16694a14c379abf2d26)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 344.15 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.12K | ± 778.63 | ops/s | 1.2x slower |
| prometheusAdd | 51.16K | ± 523.35 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.25K | ± 1.58K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.61K | ± 132.53 | ops/s | 10x slower |
| simpleclientInc | 6.54K | ± 181.00 | ops/s | 10x slower |
| simpleclientAdd | 6.06K | ± 134.15 | ops/s | 11x slower |
| openTelemetryAdd | 1.33K | ± 179.32 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.25K | ± 31.34 | ops/s | 53x slower |
| openTelemetryInc | 1.24K | ± 74.44 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.33K | ± 1.35K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 17.17 | ops/s | 1.2x slower |
| prometheusNative | 2.76K | ± 343.85 | ops/s | 1.9x slower |
| openTelemetryClassic | 693.74 | ± 25.88 | ops/s | 7.7x slower |
| openTelemetryExponential | 532.26 | ± 12.45 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.71K | ± 1.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.25K | ± 4.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.36K | ± 4.47K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.44K | ± 4.25K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49251.368   ± 1579.373  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1329.231    ± 179.324  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1242.558     ± 74.441  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1251.081     ± 31.336  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51163.272    ± 523.354  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66417.891    ± 344.155  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56124.068    ± 778.625  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6062.491    ± 134.151  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6538.423    ± 180.998  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6610.985    ± 132.533  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.744     ± 25.885  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        532.259     ± 12.451  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5332.428   ± 1351.501  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2755.146    ± 343.849  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4547.369     ± 17.172  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474440.877   ± 4253.302  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484355.779   ± 4465.550  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489250.912   ± 4408.102  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493705.875   ± 1165.979  ops/s
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
