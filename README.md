# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-11T10:29:30Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 673.86M | ± 15028.10K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.01M | ± 702.54K | ops/s |
| prometheusLabelValuesInc | 141.06M | ± 1405.78K | ops/s |
| prometheusLabelValuesIncSingleThread | 67.94M | ± 402.00K | ops/s |
| prometheusInc | 77.39K | ± 1.32K | ops/s |
| prometheusNoLabelsInc | 66.19K | ± 788.07 | ops/s |
| prometheusAdd | 62.05K | ± 494.84 | ops/s |
| codahaleIncNoLabels | 56.91K | ± 280.20 | ops/s |
| openTelemetryBoundInc | 44.63K | ± 838.50 | ops/s |
| openTelemetryBoundAdd | 38.42K | ± 64.72 | ops/s |
| openTelemetryInc | 27.56K | ± 260.03 | ops/s |
| openTelemetryIncNoLabels | 26.97K | ± 268.74 | ops/s |
| openTelemetryAdd | 24.42K | ± 648.63 | ops/s |
| simpleclientInc | 7.87K | ± 111.59 | ops/s |
| simpleclientNoLabelsInc | 7.56K | ± 23.39 | ops/s |
| simpleclientAdd | 7.20K | ± 369.87 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.56K | ± 38.11 | ops/s |
| prometheusClassic | 9.75K | ± 3.04K | ops/s |
| prometheusClassicSingleThread | 7.17K | ± 19.28 | ops/s |
| openTelemetryClassic | 6.83K | ± 885.81 | ops/s |
| openTelemetryBoundClassic | 6.44K | ± 1.50K | ops/s |
| simpleclient | 5.88K | ± 90.43 | ops/s |
| prometheusNative | 3.80K | ± 53.78 | ops/s |
| openTelemetryBoundExponential | 899.62 | ± 24.67 | ops/s |
| openTelemetryExponential | 896.01 | ± 19.70 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.51K | ± 384.78 | ops/s |
| openMetricsWriteToNull | 40.07K | ± 536.33 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 763.35K | ± 7.04K | ops/s |
| prometheusWriteToByteArray | 755.82K | ± 22.43K | ops/s |
| openMetricsWriteToNull | 715.06K | ± 7.75K | ops/s |
| openMetricsWriteToByteArray | 708.27K | ± 6.15K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.017 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.024 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.021 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.035 | — | — |
| CounterBenchmark.prometheusAdd | 0.060 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.131 | — | — |
| CounterBenchmark.simpleclientInc | 0.120 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.125 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.156 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.046 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.143 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.053 | — | — |
| HistogramBenchmark.prometheusClassic | 0.415 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.460 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.407 | — | — |
| HistogramBenchmark.prometheusNative | 417712.981 | — | — |
| HistogramBenchmark.simpleclient | 0.160 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.088 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.087 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56905.605    ± 280.201  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24423.688    ± 648.630  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38417.461     ± 64.718  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      44627.217    ± 838.503  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27558.133    ± 260.025  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      26973.708    ± 268.735  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62050.001    ± 494.841  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  673864910.000 ± 15028104.314  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370007328.816 ± 702544.759  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77392.309   ± 1316.264  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  141059061.707 ± 1405776.066  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   67941446.821 ± 401996.789  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66193.184    ± 788.070  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7204.018    ± 369.869  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7867.353    ± 111.594  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7564.305     ± 23.386  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6440.481   ± 1503.188  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        899.622     ± 24.674  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6828.036    ± 885.813  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        896.005     ± 19.697  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9752.996   ± 3037.016  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17564.576     ± 38.106  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7173.743     ± 19.275  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3801.894     ± 53.783  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5878.283     ± 90.427  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40070.899    ± 536.330  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40514.407    ± 384.782  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     708269.134   ± 6152.492  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     715062.485   ± 7754.254  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     755815.947  ± 22428.341  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     763348.693   ± 7039.032  ops/s
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
