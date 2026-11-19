# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-19T11:33:46Z
- **Commit:** [`3ea508f`](https://github.com/dhoard/client_java/commit/3ea508f61ddaa1f8b43266e3bf378d7f60e14f25)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 556.44M | ± 10068.41K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.73M | ± 343.48K | ops/s |
| prometheusLabelValuesInc | 114.94M | ± 2229.49K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.48M | ± 281.03K | ops/s |
| prometheusInc | 65.65K | ± 1.02K | ops/s |
| prometheusNoLabelsInc | 55.41K | ± 1.13K | ops/s |
| prometheusAdd | 50.68K | ± 886.80 | ops/s |
| codahaleIncNoLabels | 48.39K | ± 1.03K | ops/s |
| openTelemetryBoundInc | 37.79K | ± 728.63 | ops/s |
| openTelemetryBoundAdd | 31.64K | ± 854.10 | ops/s |
| openTelemetryIncNoLabels | 23.57K | ± 803.10 | ops/s |
| openTelemetryInc | 23.10K | ± 410.85 | ops/s |
| openTelemetryAdd | 19.36K | ± 264.70 | ops/s |
| simpleclientInc | 6.62K | ± 101.19 | ops/s |
| simpleclientAdd | 6.43K | ± 109.30 | ops/s |
| simpleclientNoLabelsInc | 6.30K | ± 90.00 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.03K | ± 176.19 | ops/s |
| prometheusClassic | 7.06K | ± 90.21 | ops/s |
| openTelemetryClassic | 4.68K | ± 1.07K | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 18.85 | ops/s |
| simpleclient | 4.47K | ± 78.13 | ops/s |
| openTelemetryBoundClassic | 3.40K | ± 484.94 | ops/s |
| prometheusNative | 2.77K | ± 328.88 | ops/s |
| openTelemetryBoundExponential | 1.09K | ± 50.61 | ops/s |
| openTelemetryExponential | 929.61 | ± 82.25 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.28K | ± 663.28 | ops/s |
| prometheusWriteToNull | 29.97K | ± 998.25 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 516.15K | ± 8.12K | ops/s |
| prometheusWriteToByteArray | 507.58K | ± 9.65K | ops/s |
| openMetricsWriteToNull | 505.19K | ± 3.33K | ops/s |
| openMetricsWriteToByteArray | 500.42K | ± 5.08K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.048 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.040 | — | — |
| CounterBenchmark.prometheusAdd | 0.073 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.146 | — | — |
| CounterBenchmark.simpleclientInc | 0.141 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.148 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.280 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.864 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.207 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.016 | — | — |
| HistogramBenchmark.prometheusClassic | 0.522 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.676 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.645 | — | — |
| HistogramBenchmark.prometheusNative | 417713.353 | — | — |
| HistogramBenchmark.simpleclient | 0.212 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.116 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.118 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18477.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48385.874   ± 1031.389  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19355.347    ± 264.701  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31637.843    ± 854.096  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37789.400    ± 728.628  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23100.506    ± 410.846  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      23569.987    ± 803.098  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50677.420    ± 886.798  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  556440854.184 ± 10068405.423  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334725323.615 ± 343477.728  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65651.740   ± 1022.214  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  114939276.609 ± 2229489.427  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58484242.680 ± 281027.957  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55413.895   ± 1130.202  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6431.003    ± 109.302  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6615.048    ± 101.191  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6296.276     ± 90.002  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       3397.974    ± 484.936  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1088.297     ± 50.613  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4684.273   ± 1067.878  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        929.615     ± 82.254  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7059.571     ± 90.210  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12027.007    ± 176.187  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4521.873     ± 18.846  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2774.315    ± 328.875  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4468.228     ± 78.127  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30278.376    ± 663.280  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      29968.938    ± 998.249  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     500418.496   ± 5079.757  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     505187.232   ± 3330.843  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     507577.817   ± 9650.000  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     516154.772   ± 8121.886  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
