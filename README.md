# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-17T08:16:59Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 722.17M | ± 30745.91K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 224.72M | ± 447.03K | ops/s |
| prometheusLabelValuesInc | 212.23M | ± 2077.47K | ops/s |
| prometheusLabelValuesIncSingleThread | 99.15M | ± 1064.11K | ops/s |
| prometheusInc | 70.02K | ± 190.16 | ops/s |
| prometheusNoLabelsInc | 65.81K | ± 1.24K | ops/s |
| codahaleIncNoLabels | 65.30K | ± 3.62K | ops/s |
| prometheusAdd | 58.47K | ± 458.78 | ops/s |
| openTelemetryBoundInc | 54.87K | ± 741.66 | ops/s |
| openTelemetryBoundAdd | 47.04K | ± 1.03K | ops/s |
| openTelemetryIncNoLabels | 37.19K | ± 342.47 | ops/s |
| openTelemetryInc | 34.77K | ± 2.56K | ops/s |
| openTelemetryAdd | 29.18K | ± 1.66K | ops/s |
| simpleclientNoLabelsInc | 11.24K | ± 137.20 | ops/s |
| simpleclientInc | 11.22K | ± 208.00 | ops/s |
| simpleclientAdd | 10.50K | ± 220.93 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.48K | ± 236.19 | ops/s |
| prometheusClassic | 10.35K | ± 1.20K | ops/s |
| openTelemetryClassic | 7.30K | ± 2.10K | ops/s |
| simpleclient | 7.05K | ± 95.78 | ops/s |
| openTelemetryBoundClassic | 6.71K | ± 2.55K | ops/s |
| prometheusNative | 4.79K | ± 384.39 | ops/s |
| prometheusClassicSingleThread | 4.44K | ± 96.17 | ops/s |
| openTelemetryBoundExponential | 1.22K | ± 33.69 | ops/s |
| openTelemetryExponential | 1.03K | ± 33.31 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 33.69K | ± 464.31 | ops/s |
| openMetricsWriteToNull | 33.29K | ± 531.71 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 797.89K | ± 60.19K | ops/s |
| prometheusWriteToByteArray | 776.25K | ± 44.88K | ops/s |
| openMetricsWriteToNull | 744.51K | ± 14.57K | ops/s |
| openMetricsWriteToByteArray | 737.99K | ± 24.01K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.033 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.017 | — | — |
| CounterBenchmark.openTelemetryInc | 0.027 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.025 | — | — |
| CounterBenchmark.prometheusAdd | 0.063 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.053 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.090 | — | — |
| CounterBenchmark.simpleclientInc | 0.084 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.084 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.157 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.778 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.142 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.918 | — | — |
| HistogramBenchmark.prometheusClassic | 0.362 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.522 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.624 | — | — |
| HistogramBenchmark.prometheusNative | 417712.796 | — | — |
| HistogramBenchmark.simpleclient | 0.134 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.106 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.105 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      65302.040   ± 3615.007  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      29184.706   ± 1658.785  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      47040.832   ± 1026.423  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      54871.251    ± 741.660  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      34769.774   ± 2557.770  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      37186.950    ± 342.473  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58474.228    ± 458.782  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  722166662.629 ± 30745909.146  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  224722708.511 ± 447029.476  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      70020.262    ± 190.159  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  212225023.420 ± 2077471.336  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   99150519.847 ± 1064106.352  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65809.351   ± 1240.161  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10496.773    ± 220.932  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11222.051    ± 208.003  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11243.754    ± 137.201  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6706.246   ± 2548.883  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1215.929     ± 33.691  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       7301.238   ± 2104.790  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1031.415     ± 33.314  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10350.437   ± 1199.668  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15483.589    ± 236.194  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4435.259     ± 96.170  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4794.121    ± 384.389  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7054.553     ± 95.780  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      33288.084    ± 531.706  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33686.742    ± 464.314  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     737985.513  ± 24014.285  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     744512.813  ± 14574.437  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     776250.415  ± 44877.480  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     797890.014  ± 60189.618  ops/s
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
