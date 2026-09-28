# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-28T09:15:59Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 75.06K | ± 2.62K | ops/s |
| prometheusNoLabelsInc | 66.07K | ± 1.14K | ops/s |
| prometheusAdd | 63.59K | ± 797.94 | ops/s |
| codahaleIncNoLabels | 57.64K | ± 852.78 | ops/s |
| openTelemetryIncNoLabels | 22.15K | ± 65.18 | ops/s |
| openTelemetryInc | 17.38K | ± 806.99 | ops/s |
| openTelemetryAdd | 15.68K | ± 162.54 | ops/s |
| simpleclientInc | 8.01K | ± 4.23 | ops/s |
| simpleclientAdd | 7.73K | ± 233.75 | ops/s |
| simpleclientNoLabelsInc | 7.61K | ± 85.89 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 18.15K | ± 22.32 | ops/s |
| prometheusClassicSingleThread | 7.53K | ± 31.74 | ops/s |
| prometheusClassic | 7.07K | ± 2.33K | ops/s |
| simpleclient | 5.80K | ± 136.97 | ops/s |
| prometheusNative | 3.82K | ± 206.82 | ops/s |
| openTelemetryClassic | 959.09 | ± 9.58 | ops/s |
| openTelemetryExponential | 847.58 | ± 44.45 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 35.16K | ± 344.87 | ops/s |
| prometheusWriteToNull | 34.58K | ± 1.10K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 696.34K | ± 7.07K | ops/s |
| prometheusWriteToByteArray | 666.32K | ± 20.26K | ops/s |
| openMetricsWriteToNull | 654.28K | ± 4.00K | ops/s |
| openMetricsWriteToByteArray | 639.82K | ± 4.69K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57642.328    ± 852.780  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15679.292    ± 162.538  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17376.051    ± 806.995  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22151.760     ± 65.184  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63587.697    ± 797.936  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75055.422   ± 2619.190  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66071.926   ± 1138.103  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7732.180    ± 233.754  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8010.187      ± 4.230  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7606.035     ± 85.886  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        959.093      ± 9.577  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        847.578     ± 44.448  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7069.142   ± 2328.268  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18150.267     ± 22.315  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7530.586     ± 31.744  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3818.152    ± 206.820  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5801.417    ± 136.971  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35164.488    ± 344.874  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34582.044   ± 1096.353  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     639817.666   ± 4691.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     654283.745   ± 4002.352  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     666316.319  ± 20259.313  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     696339.889   ± 7066.479  ops/s
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
