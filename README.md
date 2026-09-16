# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-16T08:21:50Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.16K | ± 582.43 | ops/s |
| prometheusNoLabelsInc | 56.82K | ± 299.15 | ops/s |
| prometheusAdd | 50.88K | ± 627.13 | ops/s |
| codahaleIncNoLabels | 49.25K | ± 1.53K | ops/s |
| openTelemetryIncNoLabels | 18.10K | ± 602.32 | ops/s |
| openTelemetryInc | 14.88K | ± 1.06K | ops/s |
| openTelemetryAdd | 13.00K | ± 54.61 | ops/s |
| simpleclientInc | 6.53K | ± 58.27 | ops/s |
| simpleclientNoLabelsInc | 6.43K | ± 152.70 | ops/s |
| simpleclientAdd | 6.17K | ± 176.56 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 18.30 | ops/s |
| prometheusClassic | 5.73K | ± 1.30K | ops/s |
| prometheusClassicSingleThread | 4.59K | ± 25.00 | ops/s |
| simpleclient | 4.39K | ± 81.87 | ops/s |
| prometheusNative | 2.73K | ± 357.36 | ops/s |
| openTelemetryClassic | 797.70 | ± 21.56 | ops/s |
| openTelemetryExponential | 795.42 | ± 153.91 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.18K | ± 528.07 | ops/s |
| openMetricsWriteToNull | 23.71K | ± 1.01K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 507.99K | ± 5.45K | ops/s |
| prometheusWriteToByteArray | 502.10K | ± 9.10K | ops/s |
| openMetricsWriteToNull | 490.26K | ± 1.99K | ops/s |
| openMetricsWriteToByteArray | 487.21K | ± 2.83K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49252.991   ± 1526.798  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13002.450     ± 54.612  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14883.648   ± 1062.752  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18099.572    ± 602.322  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50879.514    ± 627.129  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66160.928    ± 582.434  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56821.872    ± 299.146  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6167.868    ± 176.557  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.347     ± 58.273  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6428.307    ± 152.703  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        797.702     ± 21.562  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        795.423    ± 153.914  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5730.594   ± 1297.912  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12297.041     ± 18.304  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4590.041     ± 25.002  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2731.675    ± 357.360  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4388.938     ± 81.868  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23714.112   ± 1009.533  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24177.621    ± 528.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487209.157   ± 2832.743  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490264.274   ± 1992.932  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502101.781   ± 9101.407  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507989.323   ± 5452.847  ops/s
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
