# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T08:17:56Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.21K | ± 272.29 | ops/s |
| prometheusNoLabelsInc | 56.78K | ± 340.66 | ops/s |
| prometheusAdd | 51.03K | ± 539.97 | ops/s |
| codahaleIncNoLabels | 50.27K | ± 76.99 | ops/s |
| openTelemetryIncNoLabels | 18.56K | ± 56.60 | ops/s |
| openTelemetryInc | 14.91K | ± 187.83 | ops/s |
| openTelemetryAdd | 12.91K | ± 66.68 | ops/s |
| simpleclientInc | 6.56K | ± 39.08 | ops/s |
| simpleclientAdd | 6.44K | ± 60.00 | ops/s |
| simpleclientNoLabelsInc | 6.36K | ± 34.24 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.27K | ± 50.94 | ops/s |
| prometheusClassic | 4.84K | ± 1.31K | ops/s |
| prometheusClassicSingleThread | 4.61K | ± 16.30 | ops/s |
| simpleclient | 4.44K | ± 36.59 | ops/s |
| prometheusNative | 3.00K | ± 378.09 | ops/s |
| openTelemetryClassic | 853.30 | ± 42.01 | ops/s |
| openTelemetryExponential | 729.37 | ± 115.90 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.57K | ± 599.51 | ops/s |
| openMetricsWriteToNull | 23.51K | ± 878.42 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 509.16K | ± 2.66K | ops/s |
| prometheusWriteToNull | 505.90K | ± 5.43K | ops/s |
| openMetricsWriteToNull | 485.34K | ± 2.87K | ops/s |
| openMetricsWriteToByteArray | 482.41K | ± 4.77K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50268.267     ± 76.992  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12905.180     ± 66.678  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14912.591    ± 187.831  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18562.363     ± 56.600  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51031.580    ± 539.971  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66211.157    ± 272.293  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56783.384    ± 340.656  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6436.391     ± 60.000  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.648     ± 39.079  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6357.967     ± 34.244  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        853.302     ± 42.007  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        729.372    ± 115.897  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4838.697   ± 1306.910  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12274.033     ± 50.938  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4608.257     ± 16.295  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3004.689    ± 378.093  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.892     ± 36.595  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23512.441    ± 878.416  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23568.221    ± 599.515  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482408.555   ± 4771.113  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485335.612   ± 2865.412  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509164.285   ± 2659.383  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     505896.544   ± 5428.123  ops/s
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
