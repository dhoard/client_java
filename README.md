# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-29T09:41:52Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 688.27M | ± 31717.54K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 212.02M | ± 5164.36K | ops/s |
| prometheusLabelValuesInc | 205.44M | ± 2001.98K | ops/s |
| prometheusLabelValuesIncSingleThread | 94.75M | ± 1155.98K | ops/s |
| prometheusInc | 68.29K | ± 633.18 | ops/s |
| prometheusNoLabelsInc | 66.51K | ± 430.32 | ops/s |
| codahaleIncNoLabels | 62.44K | ± 2.95K | ops/s |
| prometheusAdd | 57.61K | ± 1.43K | ops/s |
| openTelemetryBoundInc | 54.12K | ± 334.68 | ops/s |
| openTelemetryBoundAdd | 47.94K | ± 381.28 | ops/s |
| openTelemetryIncNoLabels | 35.81K | ± 424.34 | ops/s |
| openTelemetryInc | 33.74K | ± 2.58K | ops/s |
| openTelemetryAdd | 27.52K | ± 554.60 | ops/s |
| simpleclientAdd | 10.55K | ± 201.94 | ops/s |
| simpleclientInc | 10.39K | ± 360.03 | ops/s |
| simpleclientNoLabelsInc | 10.34K | ± 449.08 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.85K | ± 213.02 | ops/s |
| prometheusClassic | 8.80K | ± 2.46K | ops/s |
| openTelemetryBoundClassic | 7.11K | ± 2.01K | ops/s |
| simpleclient | 6.92K | ± 279.08 | ops/s |
| openTelemetryClassic | 6.58K | ± 1.61K | ops/s |
| prometheusClassicSingleThread | 4.41K | ± 38.49 | ops/s |
| prometheusNative | 4.12K | ± 633.03 | ops/s |
| openTelemetryBoundExponential | 1.13K | ± 37.63 | ops/s |
| openTelemetryExponential | 1.02K | ± 18.29 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 34.85K | ± 544.63 | ops/s |
| prometheusWriteToNull | 34.66K | ± 276.87 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 827.63K | ± 21.05K | ops/s |
| prometheusWriteToNull | 762.87K | ± 45.04K | ops/s |
| openMetricsWriteToNull | 741.92K | ± 36.63K | ops/s |
| openMetricsWriteToByteArray | 700.13K | ± 25.03K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.034 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.017 | — | — |
| CounterBenchmark.openTelemetryInc | 0.028 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.026 | — | — |
| CounterBenchmark.prometheusAdd | 0.064 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.054 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.089 | — | — |
| CounterBenchmark.simpleclientInc | 0.091 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.091 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.837 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.152 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.925 | — | — |
| HistogramBenchmark.prometheusClassic | 0.455 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.541 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.625 | — | — |
| HistogramBenchmark.prometheusNative | 417712.939 | — | — |
| HistogramBenchmark.simpleclient | 0.138 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.101 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.102 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      62441.130   ± 2948.998  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      27516.043    ± 554.601  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      47942.305    ± 381.282  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      54120.290    ± 334.677  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      33736.949   ± 2577.835  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      35813.858    ± 424.344  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      57610.851   ± 1434.086  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  688273244.500 ± 31717537.591  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  212023605.529 ± 5164359.518  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      68289.327    ± 633.184  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  205435760.101 ± 2001981.095  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   94745306.178 ± 1155982.126  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66505.484    ± 430.323  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10554.833    ± 201.939  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10389.495    ± 360.033  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10336.784    ± 449.081  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       7111.844   ± 2006.519  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1129.356     ± 37.626  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6576.335   ± 1607.632  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1024.795     ± 18.287  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8796.567   ± 2460.063  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14852.728    ± 213.015  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4411.947     ± 38.495  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4122.670    ± 633.034  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6916.283    ± 279.080  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34848.887    ± 544.633  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34660.124    ± 276.875  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     700130.456  ± 25025.854  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     741917.145  ± 36631.996  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     827626.034  ± 21053.459  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     762873.714  ± 45040.701  ops/s
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
