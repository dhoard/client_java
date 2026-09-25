# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-25T08:12:24Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 59.79K | ± 1.16K | ops/s |
| prometheusNoLabelsInc | 51.24K | ± 477.78 | ops/s |
| prometheusAdd | 47.90K | ± 593.30 | ops/s |
| codahaleIncNoLabels | 43.68K | ± 1.69K | ops/s |
| openTelemetryIncNoLabels | 17.00K | ± 367.16 | ops/s |
| openTelemetryInc | 13.64K | ± 348.25 | ops/s |
| openTelemetryAdd | 12.12K | ± 112.16 | ops/s |
| simpleclientInc | 6.14K | ± 64.28 | ops/s |
| simpleclientNoLabelsInc | 6.00K | ± 162.98 | ops/s |
| simpleclientAdd | 5.81K | ± 353.65 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.07K | ± 10.63 | ops/s |
| prometheusClassicSingleThread | 5.85K | ± 19.26 | ops/s |
| prometheusClassic | 5.66K | ± 1.55K | ops/s |
| simpleclient | 4.52K | ± 57.86 | ops/s |
| prometheusNative | 3.17K | ± 37.57 | ops/s |
| openTelemetryClassic | 771.37 | ± 10.60 | ops/s |
| openTelemetryExponential | 728.90 | ± 19.67 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.61K | ± 186.95 | ops/s |
| openMetricsWriteToNull | 27.32K | ± 195.46 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 565.10K | ± 2.09K | ops/s |
| prometheusWriteToByteArray | 543.28K | ± 13.67K | ops/s |
| openMetricsWriteToNull | 521.55K | ± 12.51K | ops/s |
| openMetricsWriteToByteArray | 520.41K | ± 2.23K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43682.946   ± 1694.080  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12117.271    ± 112.159  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13636.275    ± 348.250  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17003.803    ± 367.157  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47898.614    ± 593.299  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59791.938   ± 1160.539  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51241.892    ± 477.776  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5807.162    ± 353.647  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6138.289     ± 64.281  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6002.287    ± 162.982  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        771.374     ± 10.604  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        728.895     ± 19.665  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5657.248   ± 1550.512  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14073.593     ± 10.631  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5847.175     ± 19.264  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3165.401     ± 37.573  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4515.602     ± 57.858  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27324.708    ± 195.458  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27605.959    ± 186.955  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520410.728   ± 2226.587  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521551.128  ± 12508.312  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     543281.953  ± 13670.082  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565103.845   ± 2090.368  ops/s
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
