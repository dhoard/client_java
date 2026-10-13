# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-13T10:02:40Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| codahaleIncNoLabels | 31.48K | ± 572.59 | ops/s |
| prometheusInc | 31.19K | ± 1.03K | ops/s |
| prometheusNoLabelsInc | 30.74K | ± 242.34 | ops/s |
| prometheusAdd | 29.62K | ± 309.86 | ops/s |
| openTelemetryIncNoLabels | 19.73K | ± 190.06 | ops/s |
| openTelemetryInc | 17.47K | ± 303.55 | ops/s |
| openTelemetryAdd | 15.12K | ± 212.21 | ops/s |
| simpleclientInc | 7.72K | ± 94.55 | ops/s |
| simpleclientNoLabelsInc | 7.61K | ± 95.79 | ops/s |
| simpleclientAdd | 7.50K | ± 94.02 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.90K | ± 62.78 | ops/s |
| simpleclient | 4.98K | ± 37.85 | ops/s |
| prometheusClassicSingleThread | 3.35K | ± 105.64 | ops/s |
| prometheusClassic | 2.92K | ± 676.46 | ops/s |
| prometheusNative | 2.12K | ± 287.01 | ops/s |
| openTelemetryClassic | 532.51 | ± 22.73 | ops/s |
| openTelemetryExponential | 496.90 | ± 47.49 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 20.45K | ± 464.04 | ops/s |
| prometheusWriteToNull | 20.40K | ± 151.51 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 320.28K | ± 2.22K | ops/s |
| prometheusWriteToByteArray | 316.86K | ± 4.50K | ops/s |
| openMetricsWriteToNull | 296.17K | ± 4.05K | ops/s |
| openMetricsWriteToByteArray | 295.94K | ± 2.81K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31483.760    ± 572.594  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15117.136    ± 212.210  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17471.206    ± 303.554  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      19729.038    ± 190.063  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29623.005    ± 309.859  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31185.983   ± 1025.452  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30742.424    ± 242.336  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7504.080     ± 94.020  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7721.609     ± 94.554  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7605.313     ± 95.793  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        532.514     ± 22.730  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        496.902     ± 47.491  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2919.217    ± 676.460  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7899.331     ± 62.784  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3350.413    ± 105.641  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2122.755    ± 287.010  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4977.489     ± 37.851  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      20449.683    ± 464.041  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      20398.471    ± 151.512  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295939.953   ± 2814.282  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296172.132   ± 4048.624  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316861.736   ± 4503.466  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     320280.917   ± 2217.893  ops/s
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
