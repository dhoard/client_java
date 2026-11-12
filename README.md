# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-12T10:52:58Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 676.63M | ± 16886.05K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.47M | ± 364.31K | ops/s |
| prometheusLabelValuesInc | 140.56M | ± 673.35K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.22M | ± 153.31K | ops/s |
| prometheusInc | 76.76K | ± 604.65 | ops/s |
| prometheusNoLabelsInc | 66.00K | ± 725.37 | ops/s |
| prometheusAdd | 62.70K | ± 1.03K | ops/s |
| codahaleIncNoLabels | 57.45K | ± 266.42 | ops/s |
| openTelemetryBoundInc | 43.37K | ± 2.91K | ops/s |
| openTelemetryBoundAdd | 38.10K | ± 522.95 | ops/s |
| openTelemetryInc | 27.62K | ± 158.87 | ops/s |
| openTelemetryIncNoLabels | 27.42K | ± 685.53 | ops/s |
| openTelemetryAdd | 24.05K | ± 44.20 | ops/s |
| simpleclientInc | 7.84K | ± 134.83 | ops/s |
| simpleclientNoLabelsInc | 7.66K | ± 142.35 | ops/s |
| simpleclientAdd | 7.43K | ± 359.39 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.26K | ± 70.89 | ops/s |
| prometheusClassic | 8.62K | ± 1.46K | ops/s |
| prometheusClassicSingleThread | 7.22K | ± 7.42 | ops/s |
| openTelemetryBoundClassic | 6.54K | ± 1.43K | ops/s |
| openTelemetryClassic | 5.98K | ± 1.42K | ops/s |
| simpleclient | 5.80K | ± 66.49 | ops/s |
| prometheusNative | 3.78K | ± 208.52 | ops/s |
| openTelemetryBoundExponential | 895.98 | ± 53.90 | ops/s |
| openTelemetryExponential | 845.97 | ± 42.16 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.85K | ± 220.49 | ops/s |
| openMetricsWriteToNull | 40.41K | ± 300.22 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 772.68K | ± 11.23K | ops/s |
| prometheusWriteToByteArray | 745.83K | ± 8.75K | ops/s |
| openMetricsWriteToNull | 718.05K | ± 6.13K | ops/s |
| openMetricsWriteToByteArray | 711.10K | ± 17.91K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.025 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.022 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.034 | — | — |
| CounterBenchmark.prometheusAdd | 0.059 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.127 | — | — |
| CounterBenchmark.simpleclientInc | 0.120 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.123 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.152 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.059 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.165 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.116 | — | — |
| HistogramBenchmark.prometheusClassic | 0.436 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.464 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.405 | — | — |
| HistogramBenchmark.prometheusNative | 335792.986 | — | — |
| HistogramBenchmark.simpleclient | 0.162 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.086 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57449.718    ± 266.415  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24046.919     ± 44.197  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38098.004    ± 522.945  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      43369.672   ± 2905.767  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27617.166    ± 158.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      27417.886    ± 685.527  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62695.801   ± 1029.590  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  676627266.632 ± 16886046.306  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370474582.563 ± 364311.115  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76761.996    ± 604.653  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  140563754.459 ± 673352.798  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68219482.757 ± 153308.158  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66004.821    ± 725.369  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7431.034    ± 359.385  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7841.276    ± 134.831  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7664.236    ± 142.352  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6543.212   ± 1431.790  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        895.983     ± 53.905  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5983.901   ± 1423.252  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        845.970     ± 42.157  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8623.248   ± 1464.261  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17264.936     ± 70.893  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7215.738      ± 7.417  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3777.301    ± 208.523  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5795.517     ± 66.494  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40410.626    ± 300.216  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40850.093    ± 220.485  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     711100.999  ± 17905.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     718053.069   ± 6132.829  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     745834.836   ± 8752.135  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772676.752  ± 11232.642  ops/s
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
