# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-04T08:03:52Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.01K | ± 342.91 | ops/s |
| prometheusNoLabelsInc | 56.40K | ± 171.59 | ops/s |
| prometheusAdd | 51.40K | ± 76.87 | ops/s |
| codahaleIncNoLabels | 48.27K | ± 1.85K | ops/s |
| openTelemetryIncNoLabels | 18.52K | ± 35.03 | ops/s |
| openTelemetryInc | 14.75K | ± 285.01 | ops/s |
| openTelemetryAdd | 12.96K | ± 65.29 | ops/s |
| simpleclientInc | 6.63K | ± 54.26 | ops/s |
| simpleclientNoLabelsInc | 6.37K | ± 33.53 | ops/s |
| simpleclientAdd | 6.26K | ± 246.04 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.34K | ± 72.56 | ops/s |
| prometheusClassic | 6.24K | ± 2.22K | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 28.59 | ops/s |
| simpleclient | 4.47K | ± 72.80 | ops/s |
| prometheusNative | 2.80K | ± 216.84 | ops/s |
| openTelemetryClassic | 839.98 | ± 78.09 | ops/s |
| openTelemetryExponential | 750.19 | ± 185.41 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.83K | ± 993.95 | ops/s |
| prometheusWriteToNull | 23.22K | ± 191.45 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 498.99K | ± 3.72K | ops/s |
| prometheusWriteToNull | 488.58K | ± 10.26K | ops/s |
| openMetricsWriteToNull | 479.74K | ± 7.92K | ops/s |
| openMetricsWriteToByteArray | 479.11K | ± 2.01K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48270.629   ± 1849.907  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12962.470     ± 65.288  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14747.926    ± 285.006  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18522.946     ± 35.028  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51397.586     ± 76.866  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66005.695    ± 342.911  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56401.496    ± 171.592  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6256.472    ± 246.044  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.106     ± 54.259  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6367.579     ± 33.527  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        839.983     ± 78.087  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        750.185    ± 185.406  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6243.134   ± 2218.755  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12338.825     ± 72.558  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4575.760     ± 28.594  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2797.294    ± 216.838  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.244     ± 72.798  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23826.949    ± 993.949  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23219.621    ± 191.447  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479113.881   ± 2013.628  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479741.390   ± 7917.306  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498989.536   ± 3721.216  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488584.596  ± 10263.194  ops/s
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
