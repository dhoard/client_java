# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-07T09:15:04Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.90K | ± 1.36K | ops/s |
| prometheusNoLabelsInc | 56.42K | ± 1.11K | ops/s |
| prometheusAdd | 51.50K | ± 295.00 | ops/s |
| codahaleIncNoLabels | 48.52K | ± 2.04K | ops/s |
| openTelemetryIncNoLabels | 18.54K | ± 87.29 | ops/s |
| openTelemetryInc | 15.38K | ± 196.77 | ops/s |
| openTelemetryAdd | 12.89K | ± 44.65 | ops/s |
| simpleclientInc | 6.54K | ± 48.66 | ops/s |
| simpleclientNoLabelsInc | 6.43K | ± 137.10 | ops/s |
| simpleclientAdd | 6.00K | ± 341.75 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.29K | ± 34.85 | ops/s |
| prometheusClassic | 5.49K | ± 1.44K | ops/s |
| prometheusClassicSingleThread | 4.56K | ± 22.31 | ops/s |
| simpleclient | 4.43K | ± 34.45 | ops/s |
| prometheusNative | 2.92K | ± 248.92 | ops/s |
| openTelemetryClassic | 840.59 | ± 76.38 | ops/s |
| openTelemetryExponential | 753.25 | ± 180.33 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.51K | ± 487.31 | ops/s |
| openMetricsWriteToNull | 23.07K | ± 611.44 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 481.80K | ± 3.81K | ops/s |
| prometheusWriteToByteArray | 480.74K | ± 2.14K | ops/s |
| openMetricsWriteToNull | 466.02K | ± 4.79K | ops/s |
| openMetricsWriteToByteArray | 459.10K | ± 7.52K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48524.252   ± 2038.722  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12894.408     ± 44.651  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15383.373    ± 196.770  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18536.439     ± 87.291  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51498.962    ± 294.996  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65898.345   ± 1355.399  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56418.896   ± 1106.731  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6004.777    ± 341.749  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6543.517     ± 48.663  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6434.988    ± 137.096  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        840.591     ± 76.385  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        753.247    ± 180.328  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5486.538   ± 1436.351  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12288.763     ± 34.847  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4561.718     ± 22.315  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2921.087    ± 248.917  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4434.102     ± 34.451  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23068.353    ± 611.444  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23511.484    ± 487.310  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     459101.869   ± 7519.547  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     466015.684   ± 4794.400  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     480740.561   ± 2140.760  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     481796.363   ± 3807.558  ops/s
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
