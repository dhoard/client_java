# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-03T08:01:16Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| codahaleIncNoLabels | 37.92K | ± 1.90K | ops/s |
| prometheusAdd | 35.81K | ± 365.69 | ops/s |
| prometheusNoLabelsInc | 35.34K | ± 1.35K | ops/s |
| prometheusInc | 34.59K | ± 645.36 | ops/s |
| openTelemetryIncNoLabels | 24.56K | ± 397.29 | ops/s |
| openTelemetryInc | 22.10K | ± 359.02 | ops/s |
| openTelemetryAdd | 19.63K | ± 248.51 | ops/s |
| simpleclientInc | 9.07K | ± 137.92 | ops/s |
| simpleclientNoLabelsInc | 9.00K | ± 159.50 | ops/s |
| simpleclientAdd | 8.90K | ± 81.15 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 9.24K | ± 74.76 | ops/s |
| simpleclient | 6.06K | ± 108.08 | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 50.34 | ops/s |
| prometheusClassic | 2.85K | ± 673.98 | ops/s |
| prometheusNative | 2.19K | ± 391.46 | ops/s |
| openTelemetryClassic | 526.46 | ± 8.81 | ops/s |
| openTelemetryExponential | 471.78 | ± 14.47 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.97K | ± 414.53 | ops/s |
| openMetricsWriteToNull | 24.46K | ± 477.46 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 339.07K | ± 2.44K | ops/s |
| prometheusWriteToByteArray | 337.66K | ± 3.92K | ops/s |
| openMetricsWriteToNull | 322.33K | ± 4.67K | ops/s |
| openMetricsWriteToByteArray | 319.61K | ± 3.74K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      37916.502   ± 1903.624  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19631.028    ± 248.511  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22099.167    ± 359.024  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      24562.425    ± 397.294  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      35814.260    ± 365.695  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      34593.056    ± 645.357  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      35339.338   ± 1350.188  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8895.272     ± 81.154  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9070.100    ± 137.922  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8997.852    ± 159.503  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        526.456      ± 8.808  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        471.784     ± 14.475  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2854.613    ± 673.984  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       9239.534     ± 74.757  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4537.898     ± 50.342  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2189.572    ± 391.460  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6056.898    ± 108.083  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24459.727    ± 477.459  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24972.249    ± 414.532  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     319610.503   ± 3739.415  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     322329.039   ± 4673.915  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     337663.113   ± 3918.476  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     339072.934   ± 2435.276  ops/s
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
