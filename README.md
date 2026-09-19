# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-19T08:13:20Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.89K | ± 374.71 | ops/s |
| prometheusNoLabelsInc | 56.68K | ± 426.89 | ops/s |
| prometheusAdd | 51.46K | ± 65.27 | ops/s |
| codahaleIncNoLabels | 50.61K | ± 705.86 | ops/s |
| openTelemetryIncNoLabels | 18.60K | ± 281.55 | ops/s |
| openTelemetryInc | 15.20K | ± 207.15 | ops/s |
| openTelemetryAdd | 12.81K | ± 88.92 | ops/s |
| simpleclientInc | 6.57K | ± 99.20 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 51.26 | ops/s |
| simpleclientAdd | 6.11K | ± 330.21 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.31K | ± 39.14 | ops/s |
| prometheusClassic | 6.57K | ± 753.91 | ops/s |
| prometheusClassicSingleThread | 4.56K | ± 32.81 | ops/s |
| simpleclient | 4.37K | ± 36.83 | ops/s |
| prometheusNative | 2.99K | ± 347.39 | ops/s |
| openTelemetryClassic | 842.31 | ± 59.87 | ops/s |
| openTelemetryExponential | 737.02 | ± 108.28 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.95K | ± 752.24 | ops/s |
| openMetricsWriteToNull | 22.34K | ± 1.89K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 503.48K | ± 4.97K | ops/s |
| prometheusWriteToByteArray | 498.59K | ± 2.40K | ops/s |
| openMetricsWriteToNull | 476.35K | ± 4.47K | ops/s |
| openMetricsWriteToByteArray | 475.27K | ± 3.15K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50610.392    ± 705.859  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12814.686     ± 88.918  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15203.590    ± 207.148  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18598.978    ± 281.553  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51455.443     ± 65.273  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65892.290    ± 374.709  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56679.991    ± 426.888  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6109.228    ± 330.211  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6573.053     ± 99.199  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.659     ± 51.257  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        842.308     ± 59.873  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        737.019    ± 108.282  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6572.189    ± 753.914  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12305.211     ± 39.144  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4556.434     ± 32.813  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2986.662    ± 347.390  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4371.666     ± 36.831  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22343.482   ± 1892.201  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23950.958    ± 752.239  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475272.746   ± 3146.810  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476347.311   ± 4469.566  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498589.628   ± 2398.302  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     503476.628   ± 4971.284  ops/s
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
