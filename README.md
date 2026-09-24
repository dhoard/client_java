# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-24T08:17:30Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.85K | ± 999.81 | ops/s |
| prometheusNoLabelsInc | 56.58K | ± 476.99 | ops/s |
| prometheusAdd | 51.40K | ± 328.88 | ops/s |
| codahaleIncNoLabels | 50.61K | ± 731.45 | ops/s |
| openTelemetryIncNoLabels | 18.56K | ± 317.26 | ops/s |
| openTelemetryInc | 14.70K | ± 206.90 | ops/s |
| openTelemetryAdd | 12.96K | ± 38.20 | ops/s |
| simpleclientInc | 6.56K | ± 38.46 | ops/s |
| simpleclientNoLabelsInc | 6.34K | ± 8.05 | ops/s |
| simpleclientAdd | 6.31K | ± 224.18 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.12K | ± 262.85 | ops/s |
| prometheusClassic | 7.23K | ± 2.18K | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 51.09 | ops/s |
| simpleclient | 4.38K | ± 28.77 | ops/s |
| prometheusNative | 2.98K | ± 259.90 | ops/s |
| openTelemetryExponential | 789.60 | ± 120.46 | ops/s |
| openTelemetryClassic | 750.76 | ± 28.88 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.30K | ± 621.24 | ops/s |
| openMetricsWriteToNull | 24.27K | ± 313.36 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 489.38K | ± 4.26K | ops/s |
| prometheusWriteToByteArray | 480.21K | ± 4.42K | ops/s |
| openMetricsWriteToNull | 468.34K | ± 5.02K | ops/s |
| openMetricsWriteToByteArray | 458.83K | ± 11.16K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50608.860    ± 731.446  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12959.480     ± 38.196  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14702.815    ± 206.898  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18556.217    ± 317.257  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51404.589    ± 328.883  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65854.739    ± 999.812  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56583.054    ± 476.992  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6312.408    ± 224.178  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6558.351     ± 38.463  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.229      ± 8.051  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.758     ± 28.878  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        789.604    ± 120.459  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7229.699   ± 2177.986  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12122.834    ± 262.853  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4575.521     ± 51.093  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2976.112    ± 259.898  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4376.186     ± 28.771  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24266.305    ± 313.363  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24296.800    ± 621.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458834.457  ± 11158.340  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468337.522   ± 5024.519  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480205.146   ± 4418.762  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489377.097   ± 4259.128  ops/s
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
