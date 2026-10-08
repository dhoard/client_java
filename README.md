# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-08T09:31:35Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.96K | ± 1.01K | ops/s |
| prometheusNoLabelsInc | 55.45K | ± 1.78K | ops/s |
| prometheusAdd | 51.59K | ± 164.36 | ops/s |
| codahaleIncNoLabels | 45.92K | ± 5.95K | ops/s |
| openTelemetryIncNoLabels | 18.46K | ± 203.55 | ops/s |
| openTelemetryInc | 15.25K | ± 218.96 | ops/s |
| openTelemetryAdd | 12.18K | ± 1.27K | ops/s |
| simpleclientInc | 6.55K | ± 141.95 | ops/s |
| simpleclientNoLabelsInc | 6.34K | ± 9.29 | ops/s |
| simpleclientAdd | 6.29K | ± 265.14 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.27K | ± 29.52 | ops/s |
| prometheusClassic | 5.52K | ± 1.47K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 12.48 | ops/s |
| simpleclient | 4.37K | ± 196.02 | ops/s |
| prometheusNative | 3.15K | ± 126.45 | ops/s |
| openTelemetryExponential | 936.22 | ± 21.81 | ops/s |
| openTelemetryClassic | 768.22 | ± 34.37 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.37K | ± 1.10K | ops/s |
| openMetricsWriteToNull | 23.65K | ± 1.21K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 513.79K | ± 2.60K | ops/s |
| prometheusWriteToByteArray | 509.05K | ± 6.40K | ops/s |
| openMetricsWriteToNull | 490.71K | ± 1.76K | ops/s |
| openMetricsWriteToByteArray | 488.09K | ± 1.95K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45918.389   ± 5948.604  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12180.895   ± 1269.376  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15254.701    ± 218.962  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18456.017    ± 203.554  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51590.643    ± 164.363  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64963.526   ± 1012.509  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55453.585   ± 1780.623  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6288.922    ± 265.140  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6553.761    ± 141.947  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6339.248      ± 9.290  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        768.215     ± 34.368  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        936.224     ± 21.807  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5519.595   ± 1474.489  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12265.126     ± 29.516  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4544.638     ± 12.482  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3151.001    ± 126.452  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4371.926    ± 196.018  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23652.915   ± 1211.321  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24370.499   ± 1095.061  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488091.248   ± 1952.425  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490708.950   ± 1759.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509049.606   ± 6396.240  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513788.309   ± 2604.510  ops/s
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
