# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-15T08:34:37Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 676.49M | ± 6239.59K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.06M | ± 430.00K | ops/s |
| prometheusLabelValuesInc | 139.86M | ± 3372.35K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.61M | ± 534.01K | ops/s |
| prometheusInc | 76.47K | ± 670.30 | ops/s |
| prometheusNoLabelsInc | 66.66K | ± 125.87 | ops/s |
| prometheusAdd | 62.24K | ± 1.51K | ops/s |
| codahaleIncNoLabels | 55.55K | ± 1.85K | ops/s |
| openTelemetryBoundInc | 44.76K | ± 81.47 | ops/s |
| openTelemetryBoundAdd | 38.97K | ± 352.12 | ops/s |
| openTelemetryInc | 27.44K | ± 442.07 | ops/s |
| openTelemetryIncNoLabels | 26.58K | ± 305.69 | ops/s |
| openTelemetryAdd | 24.10K | ± 46.77 | ops/s |
| simpleclientInc | 7.81K | ± 106.11 | ops/s |
| simpleclientAdd | 7.77K | ± 58.97 | ops/s |
| simpleclientNoLabelsInc | 7.42K | ± 116.64 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.49K | ± 174.17 | ops/s |
| prometheusClassic | 8.46K | ± 1.63K | ops/s |
| prometheusClassicSingleThread | 7.17K | ± 123.89 | ops/s |
| simpleclient | 5.66K | ± 114.67 | ops/s |
| openTelemetryBoundClassic | 5.24K | ± 266.45 | ops/s |
| openTelemetryClassic | 4.78K | ± 341.17 | ops/s |
| prometheusNative | 3.67K | ± 144.41 | ops/s |
| openTelemetryBoundExponential | 899.14 | ± 46.08 | ops/s |
| openTelemetryExponential | 848.64 | ± 72.98 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.32K | ± 136.42 | ops/s |
| openMetricsWriteToNull | 34.34K | ± 360.73 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 759.67K | ± 10.39K | ops/s |
| prometheusWriteToByteArray | 742.00K | ± 5.79K | ops/s |
| openMetricsWriteToNull | 697.60K | ± 7.99K | ops/s |
| openMetricsWriteToByteArray | 697.14K | ± 6.81K | ops/s |

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
| CounterBenchmark.prometheusAdd | 0.059 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.122 | — | — |
| CounterBenchmark.simpleclientInc | 0.121 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.127 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.182 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.054 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.198 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.122 | — | — |
| HistogramBenchmark.prometheusClassic | 0.456 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.464 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.407 | — | — |
| HistogramBenchmark.prometheusNative | 335793.010 | — | — |
| HistogramBenchmark.simpleclient | 0.166 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.103 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.100 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55549.836   ± 1846.437  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24099.277     ± 46.765  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38971.546    ± 352.124  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      44763.146     ± 81.469  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27443.602    ± 442.066  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      26578.830    ± 305.686  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62238.058   ± 1514.283  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  676485519.258 ± 6239593.074  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370060201.628 ± 429998.707  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76468.018    ± 670.304  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  139858268.496 ± 3372348.310  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68611524.428 ± 534006.651  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66663.709    ± 125.870  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7766.265     ± 58.971  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7808.891    ± 106.111  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7417.637    ± 116.642  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5239.856    ± 266.453  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        899.138     ± 46.080  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4780.399    ± 341.172  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        848.641     ± 72.984  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8456.308   ± 1626.980  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17489.435    ± 174.173  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7170.611    ± 123.888  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3667.379    ± 144.411  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5655.632    ± 114.671  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34336.480    ± 360.726  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35324.536    ± 136.417  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     697137.139   ± 6807.456  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     697601.154   ± 7989.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     742003.325   ± 5787.404  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     759673.740  ± 10391.025  ops/s
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
