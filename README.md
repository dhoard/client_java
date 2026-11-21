# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-21T10:53:09Z
- **Commit:** [`3ea508f`](https://github.com/dhoard/client_java/commit/3ea508f61ddaa1f8b43266e3bf378d7f60e14f25)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 537.76M | ± 21374.09K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.62M | ± 536.18K | ops/s |
| prometheusLabelValuesInc | 115.25M | ± 2432.94K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.43M | ± 185.81K | ops/s |
| prometheusInc | 64.16K | ± 1.66K | ops/s |
| prometheusNoLabelsInc | 56.14K | ± 1.08K | ops/s |
| prometheusAdd | 51.02K | ± 1.06K | ops/s |
| codahaleIncNoLabels | 48.49K | ± 1.74K | ops/s |
| openTelemetryBoundInc | 37.43K | ± 907.75 | ops/s |
| openTelemetryBoundAdd | 31.09K | ± 695.86 | ops/s |
| openTelemetryInc | 23.15K | ± 453.32 | ops/s |
| openTelemetryIncNoLabels | 22.63K | ± 1.16K | ops/s |
| openTelemetryAdd | 19.39K | ± 336.40 | ops/s |
| simpleclientInc | 6.60K | ± 99.45 | ops/s |
| simpleclientNoLabelsInc | 6.38K | ± 196.62 | ops/s |
| simpleclientAdd | 6.20K | ± 191.62 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 164.16 | ops/s |
| prometheusClassic | 6.80K | ± 209.26 | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 15.74 | ops/s |
| simpleclient | 4.42K | ± 90.87 | ops/s |
| openTelemetryClassic | 4.34K | ± 395.64 | ops/s |
| openTelemetryBoundClassic | 4.11K | ± 1.72K | ops/s |
| prometheusNative | 2.71K | ± 393.68 | ops/s |
| openTelemetryBoundExponential | 1.06K | ± 102.71 | ops/s |
| openTelemetryExponential | 1.04K | ± 52.15 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 31.53K | ± 1.02K | ops/s |
| openMetricsWriteToNull | 30.19K | ± 1.02K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 512.74K | ± 4.39K | ops/s |
| prometheusWriteToByteArray | 508.67K | ± 4.08K | ops/s |
| openMetricsWriteToByteArray | 499.80K | ± 3.28K | ops/s |
| openMetricsWriteToNull | 499.67K | ± 4.85K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.048 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.040 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.151 | — | — |
| CounterBenchmark.simpleclientInc | 0.142 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.147 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.268 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.894 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.218 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.903 | — | — |
| HistogramBenchmark.prometheusClassic | 0.544 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.672 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.642 | — | — |
| HistogramBenchmark.prometheusNative | 335792.757 | — | — |
| HistogramBenchmark.simpleclient | 0.214 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.117 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.112 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18477.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48490.800   ± 1741.005  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19389.823    ± 336.395  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31091.131    ± 695.861  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37434.692    ± 907.751  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23150.308    ± 453.322  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22625.061   ± 1160.385  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51020.623   ± 1061.308  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  537757932.671 ± 21374086.138  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334616642.505 ± 536181.334  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64157.498   ± 1658.595  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  115248135.122 ± 2432940.665  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58429721.450 ± 185806.530  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56139.549   ± 1079.362  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6198.899    ± 191.618  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6600.672     ± 99.453  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6375.252    ± 196.619  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4109.720   ± 1717.617  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1061.919    ± 102.713  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4341.912    ± 395.640  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1042.552     ± 52.155  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6796.743    ± 209.257  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11984.950    ± 164.156  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4523.408     ± 15.744  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2706.744    ± 393.675  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.057     ± 90.866  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30187.323   ± 1024.378  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      31530.312   ± 1015.336  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     499796.681   ± 3281.267  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     499673.773   ± 4854.493  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     508670.702   ± 4082.415  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512736.391   ± 4386.867  ops/s
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
