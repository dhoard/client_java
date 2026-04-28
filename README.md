# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-28T06:36:23Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 29.97K | ± 1.27K | ops/s | **fastest** |
| prometheusInc | 29.77K | ± 1.85K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.52K | ± 807.79 | ops/s | 1.0x slower |
| prometheusAdd | 28.51K | ± 227.76 | ops/s | 1.1x slower |
| simpleclientInc | 6.87K | ± 209.31 | ops/s | 4.4x slower |
| simpleclientNoLabelsInc | 6.80K | ± 93.17 | ops/s | 4.4x slower |
| simpleclientAdd | 6.74K | ± 33.80 | ops/s | 4.4x slower |
| openTelemetryAdd | 1.46K | ± 115.85 | ops/s | 21x slower |
| openTelemetryInc | 1.39K | ± 90.30 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.37K | ± 117.33 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 74.47 | ops/s | **fastest** |
| prometheusClassic | 2.81K | ± 429.78 | ops/s | 1.6x slower |
| prometheusNative | 2.09K | ± 186.49 | ops/s | 2.2x slower |
| openTelemetryClassic | 515.28 | ± 11.00 | ops/s | 8.8x slower |
| openTelemetryExponential | 396.79 | ± 23.10 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 317.48K | ± 3.23K | ops/s | **fastest** |
| prometheusWriteToByteArray | 314.68K | ± 1.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.73K | ± 1.77K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.26K | ± 3.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29519.939    ± 807.793  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1458.144    ± 115.853  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1387.096     ± 90.304  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1367.106    ± 117.332  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28512.995    ± 227.757  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29767.988   ± 1853.562  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29966.639   ± 1267.573  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6742.825     ± 33.801  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6869.664    ± 209.306  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6799.371     ± 93.166  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        515.283     ± 10.998  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        396.790     ± 23.104  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2814.967    ± 429.776  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2087.273    ± 186.494  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4535.475     ± 74.470  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295261.793   ± 3546.308  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296731.680   ± 1773.387  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314677.160   ± 1563.225  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     317479.928   ± 3232.868  ops/s
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
