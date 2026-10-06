# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-06T09:40:17Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 77.60K | ± 1.56K | ops/s |
| prometheusNoLabelsInc | 65.76K | ± 78.38 | ops/s |
| prometheusAdd | 62.59K | ± 1.13K | ops/s |
| codahaleIncNoLabels | 56.93K | ± 94.80 | ops/s |
| openTelemetryIncNoLabels | 21.99K | ± 328.65 | ops/s |
| openTelemetryInc | 18.31K | ± 375.76 | ops/s |
| openTelemetryAdd | 15.43K | ± 426.76 | ops/s |
| simpleclientAdd | 7.92K | ± 61.04 | ops/s |
| simpleclientInc | 7.91K | ± 80.48 | ops/s |
| simpleclientNoLabelsInc | 7.63K | ± 32.62 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 18.09K | ± 48.01 | ops/s |
| prometheusClassicSingleThread | 7.55K | ± 10.98 | ops/s |
| prometheusClassic | 5.90K | ± 762.37 | ops/s |
| simpleclient | 5.85K | ± 59.58 | ops/s |
| prometheusNative | 3.86K | ± 376.49 | ops/s |
| openTelemetryClassic | 1.01K | ± 85.02 | ops/s |
| openTelemetryExponential | 892.11 | ± 30.71 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.64K | ± 196.08 | ops/s |
| openMetricsWriteToNull | 35.42K | ± 300.91 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 703.03K | ± 3.95K | ops/s |
| prometheusWriteToByteArray | 682.12K | ± 11.16K | ops/s |
| openMetricsWriteToNull | 661.74K | ± 2.46K | ops/s |
| openMetricsWriteToByteArray | 642.73K | ± 3.84K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56930.837     ± 94.801  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15434.608    ± 426.759  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18307.517    ± 375.765  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21985.496    ± 328.650  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62592.036   ± 1126.466  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77602.297   ± 1555.431  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65755.538     ± 78.379  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7922.505     ± 61.036  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7906.775     ± 80.481  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7632.988     ± 32.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1009.510     ± 85.018  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        892.106     ± 30.709  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5898.212    ± 762.371  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18094.314     ± 48.015  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7545.084     ± 10.981  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3860.621    ± 376.486  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5849.281     ± 59.579  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35421.837    ± 300.910  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35636.594    ± 196.077  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     642725.841   ± 3840.480  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661743.484   ± 2456.750  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     682118.825  ± 11160.203  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     703030.640   ± 3953.978  ops/s
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
