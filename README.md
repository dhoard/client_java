# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-17T08:16:53Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.24K | ± 1.25K | ops/s |
| prometheusNoLabelsInc | 56.41K | ± 1.03K | ops/s |
| prometheusAdd | 51.38K | ± 294.38 | ops/s |
| codahaleIncNoLabels | 50.15K | ± 1.40K | ops/s |
| openTelemetryIncNoLabels | 18.40K | ± 261.47 | ops/s |
| openTelemetryInc | 14.87K | ± 139.34 | ops/s |
| openTelemetryAdd | 12.78K | ± 222.95 | ops/s |
| simpleclientInc | 6.59K | ± 94.53 | ops/s |
| simpleclientAdd | 6.45K | ± 130.16 | ops/s |
| simpleclientNoLabelsInc | 6.38K | ± 31.43 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.28K | ± 22.34 | ops/s |
| prometheusClassic | 6.35K | ± 860.01 | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 27.92 | ops/s |
| simpleclient | 4.36K | ± 28.05 | ops/s |
| prometheusNative | 2.77K | ± 301.77 | ops/s |
| openTelemetryClassic | 846.67 | ± 139.49 | ops/s |
| openTelemetryExponential | 816.56 | ± 109.83 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.76K | ± 460.48 | ops/s |
| openMetricsWriteToNull | 23.11K | ± 824.56 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 479.48K | ± 5.36K | ops/s |
| prometheusWriteToByteArray | 475.33K | ± 5.10K | ops/s |
| openMetricsWriteToNull | 455.92K | ± 7.43K | ops/s |
| openMetricsWriteToByteArray | 449.75K | ± 6.62K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50153.972   ± 1401.239  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12783.993    ± 222.947  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14872.508    ± 139.336  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18404.187    ± 261.469  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51378.311    ± 294.384  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64244.921   ± 1246.747  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56412.712   ± 1030.909  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6450.226    ± 130.160  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.730     ± 94.527  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6380.777     ± 31.435  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        846.673    ± 139.493  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        816.563    ± 109.833  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6353.389    ± 860.010  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12280.125     ± 22.341  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4575.949     ± 27.921  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2770.057    ± 301.774  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4364.934     ± 28.054  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23106.121    ± 824.557  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23757.409    ± 460.480  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     449753.493   ± 6618.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     455921.142   ± 7427.304  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475325.799   ± 5102.680  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     479483.331   ± 5360.393  ops/s
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
