# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-25T05:24:31Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.50K | ± 1.77K | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.93K | ± 1.08K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.28K | ± 168.41 | ops/s | 1.0x slower |
| prometheusAdd | 28.71K | ± 182.75 | ops/s | 1.1x slower |
| simpleclientInc | 7.10K | ± 8.47 | ops/s | 4.3x slower |
| simpleclientNoLabelsInc | 6.84K | ± 275.17 | ops/s | 4.5x slower |
| simpleclientAdd | 6.72K | ± 191.36 | ops/s | 4.5x slower |
| openTelemetryIncNoLabels | 1.39K | ± 74.08 | ops/s | 22x slower |
| openTelemetryInc | 1.39K | ± 112.24 | ops/s | 22x slower |
| openTelemetryAdd | 1.34K | ± 21.82 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 109.23 | ops/s | **fastest** |
| prometheusClassic | 2.55K | ± 244.62 | ops/s | 1.8x slower |
| prometheusNative | 2.23K | ± 183.03 | ops/s | 2.1x slower |
| openTelemetryClassic | 571.30 | ± 36.88 | ops/s | 8.0x slower |
| openTelemetryExponential | 414.75 | ± 14.91 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 327.49K | ± 658.71 | ops/s | **fastest** |
| prometheusWriteToByteArray | 324.30K | ± 1.30K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 307.03K | ± 1.86K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 305.37K | ± 1.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29276.372    ± 168.413  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1340.196     ± 21.819  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1387.229    ± 112.236  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1393.461     ± 74.081  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28712.096    ± 182.753  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30504.038   ± 1767.044  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29933.666   ± 1077.244  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6720.976    ± 191.364  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7101.476      ± 8.470  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6837.529    ± 275.167  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        571.302     ± 36.885  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        414.750     ± 14.912  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2552.372    ± 244.624  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2228.897    ± 183.029  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4584.851    ± 109.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     305374.821   ± 1497.417  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     307031.991   ± 1859.169  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     324300.308   ± 1301.403  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     327491.597    ± 658.710  ops/s
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
