# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-14T08:42:42Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 31.55K | ± 60.97 | ops/s |
| prometheusNoLabelsInc | 29.87K | ± 942.49 | ops/s |
| codahaleIncNoLabels | 29.15K | ± 1.43K | ops/s |
| prometheusAdd | 28.36K | ± 361.47 | ops/s |
| openTelemetryIncNoLabels | 17.17K | ± 161.77 | ops/s |
| openTelemetryInc | 13.49K | ± 177.58 | ops/s |
| openTelemetryAdd | 11.46K | ± 340.51 | ops/s |
| simpleclientInc | 6.76K | ± 284.63 | ops/s |
| simpleclientNoLabelsInc | 6.52K | ± 146.03 | ops/s |
| simpleclientAdd | 6.46K | ± 178.86 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.86K | ± 18.11 | ops/s |
| simpleclient | 4.30K | ± 67.03 | ops/s |
| prometheusClassicSingleThread | 3.29K | ± 86.20 | ops/s |
| prometheusClassic | 3.21K | ± 425.63 | ops/s |
| prometheusNative | 2.42K | ± 355.70 | ops/s |
| openTelemetryClassic | 649.35 | ± 31.40 | ops/s |
| openTelemetryExponential | 491.05 | ± 16.93 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 18.27K | ± 52.19 | ops/s |
| openMetricsWriteToNull | 18.26K | ± 80.55 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 319.42K | ± 2.95K | ops/s |
| prometheusWriteToNull | 319.32K | ± 6.43K | ops/s |
| openMetricsWriteToNull | 297.76K | ± 2.91K | ops/s |
| openMetricsWriteToByteArray | 297.03K | ± 1.31K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29148.837   ± 1430.296  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11464.274    ± 340.514  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13490.460    ± 177.578  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17169.989    ± 161.773  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28362.157    ± 361.467  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31549.709     ± 60.974  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29867.776    ± 942.487  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6462.276    ± 178.862  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6756.066    ± 284.630  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6516.362    ± 146.033  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        649.347     ± 31.395  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        491.053     ± 16.934  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3208.291    ± 425.628  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7863.803     ± 18.108  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3288.894     ± 86.201  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2417.521    ± 355.695  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4301.652     ± 67.026  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18259.302     ± 80.555  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18266.178     ± 52.186  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     297030.194   ± 1311.794  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     297760.118   ± 2912.119  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     319416.362   ± 2946.453  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319322.635   ± 6432.019  ops/s
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
