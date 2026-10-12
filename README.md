# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-12T09:36:35Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.53K | ± 627.19 | ops/s |
| prometheusNoLabelsInc | 64.33K | ± 981.57 | ops/s |
| codahaleIncNoLabels | 58.73K | ± 930.53 | ops/s |
| prometheusAdd | 54.25K | ± 1.29K | ops/s |
| openTelemetryIncNoLabels | 29.33K | ± 477.88 | ops/s |
| openTelemetryInc | 25.09K | ± 228.91 | ops/s |
| openTelemetryAdd | 21.11K | ± 764.95 | ops/s |
| simpleclientInc | 10.51K | ± 244.64 | ops/s |
| simpleclientNoLabelsInc | 10.41K | ± 594.71 | ops/s |
| simpleclientAdd | 9.90K | ± 345.88 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.71K | ± 166.17 | ops/s |
| prometheusClassic | 9.85K | ± 62.94 | ops/s |
| simpleclient | 6.84K | ± 129.80 | ops/s |
| prometheusNative | 4.72K | ± 414.31 | ops/s |
| prometheusClassicSingleThread | 4.34K | ± 61.71 | ops/s |
| openTelemetryClassic | 958.26 | ± 29.10 | ops/s |
| openTelemetryExponential | 860.17 | ± 56.19 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 32.51K | ± 337.75 | ops/s |
| openMetricsWriteToNull | 32.10K | ± 608.89 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 717.35K | ± 49.11K | ops/s |
| prometheusWriteToNull | 697.01K | ± 9.23K | ops/s |
| openMetricsWriteToNull | 661.65K | ± 59.89K | ops/s |
| openMetricsWriteToByteArray | 616.02K | ± 19.01K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      58728.519    ± 930.527  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      21108.140    ± 764.946  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      25093.742    ± 228.909  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      29334.624    ± 477.877  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      54252.079   ± 1292.853  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64527.276    ± 627.194  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64328.513    ± 981.566  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9897.126    ± 345.884  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10513.564    ± 244.645  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10413.324    ± 594.708  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        958.261     ± 29.098  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        860.173     ± 56.195  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9854.579     ± 62.936  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14710.847    ± 166.173  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4341.472     ± 61.712  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4720.221    ± 414.312  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6835.894    ± 129.799  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32101.936    ± 608.890  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32512.667    ± 337.746  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     616020.495  ± 19013.505  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661654.826  ± 59886.680  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     717350.645  ± 49112.439  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     697013.759   ± 9234.127  ops/s
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
