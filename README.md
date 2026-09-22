# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-22T08:22:48Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 63.29K | ± 4.20K | ops/s |
| prometheusNoLabelsInc | 56.50K | ± 943.72 | ops/s |
| prometheusAdd | 51.27K | ± 781.65 | ops/s |
| codahaleIncNoLabels | 49.51K | ± 1.08K | ops/s |
| openTelemetryIncNoLabels | 18.60K | ± 56.75 | ops/s |
| openTelemetryInc | 14.72K | ± 206.87 | ops/s |
| openTelemetryAdd | 12.81K | ± 66.37 | ops/s |
| simpleclientInc | 6.58K | ± 8.04 | ops/s |
| simpleclientAdd | 6.46K | ± 17.88 | ops/s |
| simpleclientNoLabelsInc | 6.39K | ± 18.11 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 18.33 | ops/s |
| prometheusClassic | 6.72K | ± 1.27K | ops/s |
| prometheusClassicSingleThread | 4.51K | ± 109.91 | ops/s |
| simpleclient | 4.41K | ± 59.40 | ops/s |
| prometheusNative | 2.98K | ± 254.05 | ops/s |
| openTelemetryClassic | 870.79 | ± 69.18 | ops/s |
| openTelemetryExponential | 695.55 | ± 76.82 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.84K | ± 757.23 | ops/s |
| openMetricsWriteToNull | 23.47K | ± 793.71 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 506.08K | ± 6.57K | ops/s |
| prometheusWriteToByteArray | 503.31K | ± 8.82K | ops/s |
| openMetricsWriteToNull | 484.80K | ± 2.78K | ops/s |
| openMetricsWriteToByteArray | 484.04K | ± 5.25K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49512.504   ± 1079.292  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12812.335     ± 66.374  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14720.960    ± 206.865  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18598.738     ± 56.751  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51267.323    ± 781.654  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63285.825   ± 4196.052  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56504.138    ± 943.721  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6455.746     ± 17.884  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6584.986      ± 8.037  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6388.023     ± 18.109  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        870.787     ± 69.184  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        695.551     ± 76.824  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6717.055   ± 1271.813  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12298.787     ± 18.325  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4514.559    ± 109.908  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2979.270    ± 254.048  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.494     ± 59.401  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23474.686    ± 793.712  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23835.986    ± 757.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484036.995   ± 5247.640  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484803.436   ± 2784.900  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503306.251   ± 8818.443  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506082.272   ± 6574.682  ops/s
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
