# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T08:37:05Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 60.09K | ± 944.25 | ops/s |
| prometheusAdd | 48.38K | ± 109.21 | ops/s |
| prometheusNoLabelsInc | 48.10K | ± 2.19K | ops/s |
| codahaleIncNoLabels | 40.46K | ± 5.61K | ops/s |
| openTelemetryIncNoLabels | 17.00K | ± 298.35 | ops/s |
| openTelemetryInc | 13.85K | ± 285.07 | ops/s |
| openTelemetryAdd | 12.20K | ± 27.76 | ops/s |
| simpleclientInc | 6.15K | ± 51.50 | ops/s |
| simpleclientAdd | 6.14K | ± 54.32 | ops/s |
| simpleclientNoLabelsInc | 5.92K | ± 25.70 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.03K | ± 45.54 | ops/s |
| prometheusClassicSingleThread | 5.86K | ± 10.37 | ops/s |
| prometheusClassic | 4.64K | ± 651.75 | ops/s |
| simpleclient | 4.52K | ± 67.64 | ops/s |
| prometheusNative | 3.02K | ± 290.65 | ops/s |
| openTelemetryClassic | 780.89 | ± 16.16 | ops/s |
| openTelemetryExponential | 684.38 | ± 38.47 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.56K | ± 186.48 | ops/s |
| openMetricsWriteToNull | 27.23K | ± 378.85 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 580.51K | ± 2.56K | ops/s |
| prometheusWriteToByteArray | 562.68K | ± 15.87K | ops/s |
| openMetricsWriteToNull | 548.55K | ± 3.69K | ops/s |
| openMetricsWriteToByteArray | 535.16K | ± 2.53K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40462.918   ± 5611.197  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12199.883     ± 27.761  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13852.408    ± 285.073  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16995.212    ± 298.346  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48375.666    ± 109.205  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60092.862    ± 944.251  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      48099.773   ± 2186.264  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6141.371     ± 54.323  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6152.709     ± 51.498  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5920.702     ± 25.702  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.890     ± 16.160  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        684.383     ± 38.471  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4639.982    ± 651.746  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14029.847     ± 45.536  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5855.156     ± 10.370  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3016.740    ± 290.648  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4515.279     ± 67.638  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27226.215    ± 378.851  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27564.894    ± 186.478  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535155.252   ± 2533.262  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548546.884   ± 3694.684  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     562684.038  ± 15867.928  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     580505.020   ± 2563.380  ops/s
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
