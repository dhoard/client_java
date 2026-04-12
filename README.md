# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-12T05:53:16Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.52K | ± 16.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.21K | ± 261.40 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.36K | ± 1.79K | ops/s | 1.0x slower |
| prometheusAdd | 28.46K | ± 43.65 | ops/s | 1.1x slower |
| simpleclientInc | 6.84K | ± 114.27 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.60K | ± 324.67 | ops/s | 4.8x slower |
| simpleclientAdd | 6.40K | ± 263.19 | ops/s | 4.9x slower |
| openTelemetryIncNoLabels | 1.47K | ± 81.92 | ops/s | 21x slower |
| openTelemetryInc | 1.43K | ± 27.51 | ops/s | 22x slower |
| openTelemetryAdd | 1.37K | ± 35.65 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.43K | ± 48.69 | ops/s | **fastest** |
| prometheusClassic | 3.40K | ± 487.29 | ops/s | 1.3x slower |
| prometheusNative | 2.26K | ± 142.01 | ops/s | 2.0x slower |
| openTelemetryClassic | 524.06 | ± 12.26 | ops/s | 8.5x slower |
| openTelemetryExponential | 432.07 | ± 22.08 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 319.03K | ± 1.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.80K | ± 1.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.85K | ± 2.30K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.81K | ± 2.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30355.812   ± 1790.892  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1366.503     ± 35.650  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1429.956     ± 27.509  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1474.636     ± 81.915  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28463.822     ± 43.649  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31517.607     ± 16.207  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31211.003    ± 261.399  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6402.574    ± 263.190  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6844.365    ± 114.268  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6602.190    ± 324.673  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        524.056     ± 12.263  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        432.075     ± 22.076  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3403.697    ± 487.289  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2257.799    ± 142.007  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.695     ± 48.692  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294813.467   ± 2286.993  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296849.917   ± 2302.253  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315803.876   ± 1256.674  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319034.279   ± 1453.527  ops/s
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
