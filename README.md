# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-05T09:14:50Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.37K | ± 1.61K | ops/s |
| prometheusNoLabelsInc | 56.54K | ± 320.30 | ops/s |
| prometheusAdd | 51.38K | ± 191.02 | ops/s |
| codahaleIncNoLabels | 47.24K | ± 401.87 | ops/s |
| openTelemetryIncNoLabels | 18.05K | ± 788.09 | ops/s |
| openTelemetryInc | 14.81K | ± 362.90 | ops/s |
| openTelemetryAdd | 12.72K | ± 233.84 | ops/s |
| simpleclientInc | 6.58K | ± 12.65 | ops/s |
| simpleclientAdd | 6.41K | ± 34.78 | ops/s |
| simpleclientNoLabelsInc | 6.37K | ± 29.35 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.28K | ± 35.46 | ops/s |
| prometheusClassic | 6.29K | ± 754.36 | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 49.57 | ops/s |
| simpleclient | 4.40K | ± 27.14 | ops/s |
| prometheusNative | 2.73K | ± 275.21 | ops/s |
| openTelemetryExponential | 866.78 | ± 69.25 | ops/s |
| openTelemetryClassic | 844.02 | ± 107.36 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.90K | ± 822.10 | ops/s |
| prometheusWriteToNull | 23.57K | ± 387.62 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 499.20K | ± 6.57K | ops/s |
| prometheusWriteToByteArray | 490.47K | ± 8.67K | ops/s |
| openMetricsWriteToByteArray | 475.51K | ± 2.93K | ops/s |
| openMetricsWriteToNull | 473.89K | ± 7.56K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47240.962    ± 401.875  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12719.250    ± 233.843  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14809.183    ± 362.900  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18051.512    ± 788.088  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51381.368    ± 191.017  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64372.183   ± 1611.129  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56543.818    ± 320.298  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6407.314     ± 34.781  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.941     ± 12.654  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6371.977     ± 29.352  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        844.022    ± 107.364  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        866.785     ± 69.252  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6285.387    ± 754.359  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12278.258     ± 35.458  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4582.483     ± 49.572  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2732.889    ± 275.215  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4395.335     ± 27.142  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23904.240    ± 822.101  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23566.453    ± 387.621  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475509.964   ± 2926.306  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473888.645   ± 7556.884  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490468.968   ± 8672.167  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499202.287   ± 6570.379  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
