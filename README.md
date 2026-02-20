# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-20T05:20:17Z
- **Commit:** [`0d800d0`](https://github.com/dhoard/client_java/commit/0d800d0a91578e48f34909472c183174fdf1d83e)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.64K | ± 29.10 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.01K | ± 1.77K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.74K | ± 1.30K | ops/s | 1.1x slower |
| prometheusAdd | 28.64K | ± 165.73 | ops/s | 1.1x slower |
| simpleclientInc | 6.94K | ± 79.10 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.90K | ± 331.80 | ops/s | 4.6x slower |
| simpleclientAdd | 6.63K | ± 261.91 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.38K | ± 156.47 | ops/s | 23x slower |
| openTelemetryInc | 1.37K | ± 56.38 | ops/s | 23x slower |
| openTelemetryAdd | 1.36K | ± 43.20 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.54K | ± 38.50 | ops/s | **fastest** |
| prometheusClassic | 3.60K | ± 1.19K | ops/s | 1.3x slower |
| prometheusNative | 2.38K | ± 136.31 | ops/s | 1.9x slower |
| openTelemetryClassic | 530.30 | ± 19.13 | ops/s | 8.6x slower |
| openTelemetryExponential | 401.47 | ± 12.53 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 322.12K | ± 1.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 316.63K | ± 1.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.61K | ± 4.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 297.95K | ± 1.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28737.806   ± 1304.270  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1355.155     ± 43.202  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1373.287     ± 56.379  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1378.715    ± 156.474  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28642.138    ± 165.732  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31639.618     ± 29.102  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30011.420   ± 1772.333  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6633.292    ± 261.910  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6944.034     ± 79.104  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6896.060    ± 331.799  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        530.303     ± 19.130  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        401.467     ± 12.535  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3595.692   ± 1185.022  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2378.050    ± 136.308  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4543.866     ± 38.499  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297949.839   ± 1500.721  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299606.389   ± 4631.277  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316633.298   ± 1467.979  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     322123.526   ± 1706.325  ops/s
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
