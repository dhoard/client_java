# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-21T08:39:58Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 548.06M | ± 15284.14K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.31M | ± 328.73K | ops/s |
| prometheusLabelValuesInc | 114.37M | ± 1972.93K | ops/s |
| prometheusLabelValuesIncSingleThread | 57.91M | ± 835.52K | ops/s |
| prometheusInc | 65.55K | ± 1.32K | ops/s |
| prometheusNoLabelsInc | 55.45K | ± 1.18K | ops/s |
| prometheusAdd | 51.26K | ± 619.27 | ops/s |
| codahaleIncNoLabels | 49.02K | ± 1.77K | ops/s |
| openTelemetryBoundInc | 37.41K | ± 595.81 | ops/s |
| openTelemetryBoundAdd | 31.55K | ± 788.24 | ops/s |
| openTelemetryInc | 23.14K | ± 318.17 | ops/s |
| openTelemetryIncNoLabels | 22.04K | ± 1.22K | ops/s |
| openTelemetryAdd | 19.32K | ± 327.84 | ops/s |
| simpleclientInc | 6.48K | ± 112.17 | ops/s |
| simpleclientNoLabelsInc | 6.27K | ± 107.78 | ops/s |
| simpleclientAdd | 6.15K | ± 202.97 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.00K | ± 170.52 | ops/s |
| prometheusClassic | 7.64K | ± 1.13K | ops/s |
| prometheusClassicSingleThread | 4.51K | ± 18.99 | ops/s |
| simpleclient | 4.44K | ± 74.72 | ops/s |
| openTelemetryBoundClassic | 4.01K | ± 627.09 | ops/s |
| openTelemetryClassic | 3.60K | ± 167.11 | ops/s |
| prometheusNative | 2.60K | ± 224.81 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 48.91 | ops/s |
| openTelemetryExponential | 966.13 | ± 68.62 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.42K | ± 644.35 | ops/s |
| prometheusWriteToNull | 23.25K | ± 757.02 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 478.39K | ± 5.53K | ops/s |
| prometheusWriteToByteArray | 467.02K | ± 9.67K | ops/s |
| openMetricsWriteToNull | 461.41K | ± 14.30K | ops/s |
| openMetricsWriteToByteArray | 456.10K | ± 7.86K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.049 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.152 | — | — |
| CounterBenchmark.simpleclientInc | 0.145 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.238 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.895 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.261 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.977 | — | — |
| HistogramBenchmark.prometheusClassic | 0.489 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.677 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.647 | — | — |
| HistogramBenchmark.prometheusNative | 417713.423 | — | — |
| HistogramBenchmark.simpleclient | 0.214 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.151 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.152 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49021.634   ± 1767.644  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19319.947    ± 327.845  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31551.504    ± 788.235  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37409.971    ± 595.809  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23140.972    ± 318.169  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22040.341   ± 1215.256  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51255.416    ± 619.271  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  548063402.604 ± 15284140.484  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334311402.054 ± 328733.338  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65553.970   ± 1323.145  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  114374860.004 ± 1972933.958  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   57907627.642 ± 835520.187  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55449.664   ± 1176.256  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6152.467    ± 202.967  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6483.382    ± 112.166  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6269.738    ± 107.780  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4010.679    ± 627.087  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1051.072     ± 48.906  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3603.047    ± 167.110  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        966.129     ± 68.620  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7638.453   ± 1126.728  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12004.797    ± 170.519  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4514.194     ± 18.985  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2602.918    ± 224.813  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4439.867     ± 74.717  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23423.424    ± 644.351  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23249.325    ± 757.022  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456101.638   ± 7860.010  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     461406.730  ± 14301.552  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     467019.354   ± 9668.793  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     478390.395   ± 5529.826  ops/s
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
