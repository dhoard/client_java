# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-21T08:46:28Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| codahaleIncNoLabels | 30.70K | ± 902.56 | ops/s |
| prometheusInc | 30.14K | ± 104.22 | ops/s |
| prometheusNoLabelsInc | 29.92K | ± 569.62 | ops/s |
| prometheusAdd | 28.65K | ± 441.61 | ops/s |
| openTelemetryIncNoLabels | 19.18K | ± 269.53 | ops/s |
| openTelemetryInc | 17.31K | ± 169.68 | ops/s |
| openTelemetryAdd | 14.36K | ± 286.10 | ops/s |
| simpleclientInc | 7.52K | ± 119.85 | ops/s |
| simpleclientNoLabelsInc | 7.33K | ± 156.04 | ops/s |
| simpleclientAdd | 7.08K | ± 84.65 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.60K | ± 119.04 | ops/s |
| simpleclient | 4.72K | ± 44.44 | ops/s |
| prometheusClassic | 3.77K | ± 2.12K | ops/s |
| prometheusClassicSingleThread | 3.27K | ± 96.11 | ops/s |
| prometheusNative | 2.17K | ± 133.07 | ops/s |
| openTelemetryClassic | 526.63 | ± 38.70 | ops/s |
| openTelemetryExponential | 483.84 | ± 69.83 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 19.83K | ± 85.65 | ops/s |
| openMetricsWriteToNull | 19.72K | ± 176.58 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 316.78K | ± 1.71K | ops/s |
| prometheusWriteToByteArray | 316.04K | ± 2.12K | ops/s |
| openMetricsWriteToNull | 296.41K | ± 4.44K | ops/s |
| openMetricsWriteToByteArray | 288.08K | ± 1.76K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30700.005    ± 902.558  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      14363.289    ± 286.097  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17308.189    ± 169.677  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      19176.962    ± 269.532  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28649.284    ± 441.606  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30141.126    ± 104.223  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29923.491    ± 569.619  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7077.329     ± 84.654  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7519.567    ± 119.854  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7333.769    ± 156.039  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        526.627     ± 38.699  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        483.840     ± 69.834  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3771.764   ± 2116.651  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7598.086    ± 119.042  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3273.969     ± 96.110  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2170.615    ± 133.065  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4721.657     ± 44.440  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      19720.940    ± 176.579  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19828.715     ± 85.651  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     288080.851   ± 1759.554  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296408.142   ± 4440.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316036.707   ± 2121.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     316784.012   ± 1707.322  ops/s
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
