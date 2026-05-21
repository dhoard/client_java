# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-21T07:17:32Z
- **Commit:** [`0bc0408`](https://github.com/dhoard/client_java/commit/0bc040814f37610ca3bb7b1f1474dbecdb20668d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.54K | ± 42.28 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.18K | ± 935.42 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.33K | ± 1.22K | ops/s | 1.1x slower |
| prometheusAdd | 28.42K | ± 44.84 | ops/s | 1.1x slower |
| simpleclientInc | 6.91K | ± 38.04 | ops/s | 4.6x slower |
| simpleclientAdd | 6.50K | ± 142.18 | ops/s | 4.9x slower |
| simpleclientNoLabelsInc | 6.36K | ± 241.45 | ops/s | 5.0x slower |
| openTelemetryIncNoLabels | 2.74K | ± 244.75 | ops/s | 12x slower |
| openTelemetryAdd | 2.45K | ± 305.15 | ops/s | 13x slower |
| openTelemetryInc | 2.32K | ± 125.46 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 43.19 | ops/s | **fastest** |
| prometheusClassic | 3.44K | ± 1.15K | ops/s | 1.3x slower |
| prometheusNative | 2.18K | ± 160.21 | ops/s | 2.0x slower |
| openTelemetryClassic | 594.19 | ± 20.95 | ops/s | 7.5x slower |
| openTelemetryExponential | 487.64 | ± 16.48 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.32K | ± 52.95 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.14K | ± 85.78 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.73K | ± 3.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 314.94K | ± 3.95K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 291.97K | ± 3.43K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 288.70K | ± 2.27K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29325.084   ± 1223.644  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2448.621    ± 305.148  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2322.580    ± 125.456  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2735.247    ± 244.753  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28421.290     ± 44.843  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31539.804     ± 42.285  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31175.609    ± 935.418  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6502.177    ± 142.184  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6909.902     ± 38.039  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6364.198    ± 241.452  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        594.186     ± 20.954  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        487.635     ± 16.481  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3442.907   ± 1150.986  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2184.136    ± 160.208  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4456.781     ± 43.194  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18139.323     ± 85.783  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18317.140     ± 52.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     288698.221   ± 2271.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     291965.304   ± 3432.038  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314937.671   ± 3952.260  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318729.380   ± 3684.966  ops/s
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
