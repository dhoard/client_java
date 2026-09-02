# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-02T07:57:09Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| codahaleIncNoLabels | 27.52K | ± 204.89 | ops/s |
| prometheusInc | 26.56K | ± 25.48 | ops/s |
| prometheusNoLabelsInc | 26.35K | ± 253.82 | ops/s |
| prometheusAdd | 25.86K | ± 58.08 | ops/s |
| openTelemetryIncNoLabels | 17.01K | ± 60.58 | ops/s |
| openTelemetryInc | 15.21K | ± 52.23 | ops/s |
| openTelemetryAdd | 13.27K | ± 94.16 | ops/s |
| simpleclientInc | 6.74K | ± 42.39 | ops/s |
| simpleclientNoLabelsInc | 6.62K | ± 65.79 | ops/s |
| simpleclientAdd | 6.41K | ± 103.18 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 6.81K | ± 54.65 | ops/s |
| simpleclient | 4.34K | ± 43.23 | ops/s |
| prometheusClassicSingleThread | 2.92K | ± 93.28 | ops/s |
| prometheusClassic | 2.73K | ± 935.30 | ops/s |
| prometheusNative | 2.20K | ± 230.08 | ops/s |
| openTelemetryClassic | 489.31 | ± 64.97 | ops/s |
| openTelemetryExponential | 466.19 | ± 45.86 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 17.95K | ± 75.40 | ops/s |
| prometheusWriteToNull | 16.75K | ± 752.72 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 307.12K | ± 1.12K | ops/s |
| prometheusWriteToByteArray | 304.49K | ± 1.41K | ops/s |
| openMetricsWriteToNull | 286.75K | ± 1.59K | ops/s |
| openMetricsWriteToByteArray | 285.86K | ± 786.24 | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27516.320    ± 204.886  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13268.506     ± 94.160  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15205.870     ± 52.226  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17009.166     ± 60.576  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25862.854     ± 58.082  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26556.819     ± 25.480  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26352.591    ± 253.822  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6405.414    ± 103.180  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6737.104     ± 42.390  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6623.499     ± 65.786  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        489.309     ± 64.973  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        466.192     ± 45.864  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2727.911    ± 935.297  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6811.252     ± 54.654  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2917.879     ± 93.278  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2203.864    ± 230.078  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4341.826     ± 43.230  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17951.463     ± 75.397  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      16747.009    ± 752.717  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     285860.798    ± 786.243  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     286745.472   ± 1586.166  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     304488.903   ± 1412.645  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     307115.455   ± 1120.867  ops/s
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
