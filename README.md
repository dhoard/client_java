# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T09:20:31Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusNoLabelsInc | 26.16K | ± 318.73 | ops/s |
| codahaleIncNoLabels | 25.95K | ± 1.65K | ops/s |
| prometheusInc | 25.94K | ± 368.98 | ops/s |
| prometheusAdd | 25.49K | ± 83.87 | ops/s |
| openTelemetryIncNoLabels | 16.65K | ± 156.28 | ops/s |
| openTelemetryInc | 15.08K | ± 138.19 | ops/s |
| openTelemetryAdd | 13.04K | ± 84.90 | ops/s |
| simpleclientInc | 6.65K | ± 66.67 | ops/s |
| simpleclientNoLabelsInc | 6.55K | ± 29.63 | ops/s |
| simpleclientAdd | 6.43K | ± 38.64 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 6.68K | ± 86.11 | ops/s |
| simpleclient | 4.25K | ± 17.54 | ops/s |
| prometheusClassicSingleThread | 2.88K | ± 82.17 | ops/s |
| prometheusClassic | 2.67K | ± 354.25 | ops/s |
| prometheusNative | 2.15K | ± 114.08 | ops/s |
| openTelemetryClassic | 518.19 | ± 41.32 | ops/s |
| openTelemetryExponential | 404.19 | ± 25.96 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 17.78K | ± 58.13 | ops/s |
| openMetricsWriteToNull | 17.65K | ± 56.16 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 303.39K | ± 1.47K | ops/s |
| prometheusWriteToByteArray | 301.96K | ± 639.50 | ops/s |
| openMetricsWriteToNull | 283.52K | ± 2.83K | ops/s |
| openMetricsWriteToByteArray | 281.94K | ± 1.26K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      25952.836   ± 1652.602  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13035.400     ± 84.899  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15079.425    ± 138.185  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16648.186    ± 156.275  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25494.483     ± 83.872  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      25941.831    ± 368.981  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26155.029    ± 318.729  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6432.659     ± 38.641  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6654.578     ± 66.674  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6554.976     ± 29.630  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        518.186     ± 41.316  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        404.194     ± 25.960  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2669.616    ± 354.248  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6684.094     ± 86.114  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2876.655     ± 82.172  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2148.632    ± 114.079  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4249.139     ± 17.543  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17650.039     ± 56.164  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17782.260     ± 58.133  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     281938.866   ± 1261.777  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     283516.233   ± 2830.180  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     301959.347    ± 639.501  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     303393.296   ± 1473.731  ops/s
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
