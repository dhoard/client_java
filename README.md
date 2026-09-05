# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-05T07:50:28Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.73K | ± 731.13 | ops/s |
| prometheusNoLabelsInc | 55.97K | ± 810.16 | ops/s |
| prometheusAdd | 51.38K | ± 142.77 | ops/s |
| codahaleIncNoLabels | 49.50K | ± 531.59 | ops/s |
| openTelemetryIncNoLabels | 18.42K | ± 139.94 | ops/s |
| openTelemetryInc | 14.99K | ± 241.91 | ops/s |
| openTelemetryAdd | 12.97K | ± 27.73 | ops/s |
| simpleclientInc | 6.55K | ± 45.21 | ops/s |
| simpleclientNoLabelsInc | 6.38K | ± 194.62 | ops/s |
| simpleclientAdd | 6.30K | ± 140.74 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 17.78 | ops/s |
| prometheusClassic | 6.56K | ± 1.06K | ops/s |
| prometheusClassicSingleThread | 4.53K | ± 29.63 | ops/s |
| simpleclient | 4.40K | ± 91.48 | ops/s |
| prometheusNative | 2.93K | ± 292.54 | ops/s |
| openTelemetryClassic | 789.61 | ± 15.26 | ops/s |
| openTelemetryExponential | 755.38 | ± 204.05 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.98K | ± 507.15 | ops/s |
| openMetricsWriteToNull | 23.91K | ± 378.24 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 514.81K | ± 2.51K | ops/s |
| prometheusWriteToByteArray | 504.72K | ± 6.26K | ops/s |
| openMetricsWriteToNull | 491.60K | ± 2.43K | ops/s |
| openMetricsWriteToByteArray | 484.96K | ± 1.55K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49498.631    ± 531.586  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12965.341     ± 27.733  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14988.925    ± 241.913  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18421.829    ± 139.936  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51381.487    ± 142.768  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66726.834    ± 731.133  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55973.590    ± 810.164  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6299.600    ± 140.742  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6554.961     ± 45.210  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6378.824    ± 194.616  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        789.614     ± 15.264  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        755.377    ± 204.047  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6559.839   ± 1062.205  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12295.572     ± 17.782  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4529.727     ± 29.632  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2928.156    ± 292.542  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4403.102     ± 91.481  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23906.530    ± 378.236  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23975.669    ± 507.155  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484964.545   ± 1553.433  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491598.668   ± 2432.036  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     504721.387   ± 6261.331  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     514806.282   ± 2511.300  ops/s
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
