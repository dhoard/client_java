# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T08:11:09Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.98K | ± 350.41 | ops/s |
| prometheusNoLabelsInc | 56.91K | ± 380.28 | ops/s |
| prometheusAdd | 51.46K | ± 275.68 | ops/s |
| codahaleIncNoLabels | 49.91K | ± 339.78 | ops/s |
| openTelemetryIncNoLabels | 18.53K | ± 96.49 | ops/s |
| openTelemetryInc | 15.28K | ± 241.31 | ops/s |
| openTelemetryAdd | 12.84K | ± 139.23 | ops/s |
| simpleclientInc | 6.58K | ± 10.11 | ops/s |
| simpleclientNoLabelsInc | 6.33K | ± 46.15 | ops/s |
| simpleclientAdd | 6.33K | ± 182.04 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.31K | ± 13.05 | ops/s |
| prometheusClassicSingleThread | 4.57K | ± 38.07 | ops/s |
| simpleclient | 4.41K | ± 36.06 | ops/s |
| prometheusClassic | 4.21K | ± 320.60 | ops/s |
| prometheusNative | 3.26K | ± 34.01 | ops/s |
| openTelemetryClassic | 861.99 | ± 107.74 | ops/s |
| openTelemetryExponential | 847.95 | ± 146.29 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 24.28K | ± 646.93 | ops/s |
| prometheusWriteToNull | 23.83K | ± 1.25K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 509.42K | ± 2.26K | ops/s |
| prometheusWriteToByteArray | 496.52K | ± 6.09K | ops/s |
| openMetricsWriteToNull | 482.54K | ± 5.03K | ops/s |
| openMetricsWriteToByteArray | 476.12K | ± 2.98K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49906.433    ± 339.784  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12844.533    ± 139.231  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15278.984    ± 241.313  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18527.650     ± 96.486  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51461.366    ± 275.678  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65979.946    ± 350.408  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56905.728    ± 380.276  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6332.019    ± 182.042  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.013     ± 10.106  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6332.994     ± 46.149  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        861.995    ± 107.740  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        847.945    ± 146.289  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4207.086    ± 320.604  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12305.683     ± 13.046  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4567.311     ± 38.074  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3261.232     ± 34.011  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4406.847     ± 36.056  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24284.115    ± 646.927  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23829.579   ± 1247.365  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476117.412   ± 2975.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482539.736   ± 5033.723  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496518.045   ± 6086.793  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509423.440   ± 2262.367  ops/s
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
