# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-16T08:28:48Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 548.04M | ± 12559.98K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.79M | ± 151.18K | ops/s |
| prometheusLabelValuesInc | 116.03M | ± 1606.09K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.51M | ± 125.91K | ops/s |
| prometheusInc | 65.39K | ± 1.56K | ops/s |
| prometheusNoLabelsInc | 56.13K | ± 1.50K | ops/s |
| prometheusAdd | 50.77K | ± 1.08K | ops/s |
| codahaleIncNoLabels | 48.56K | ± 2.25K | ops/s |
| openTelemetryBoundInc | 36.17K | ± 2.93K | ops/s |
| openTelemetryBoundAdd | 31.33K | ± 794.61 | ops/s |
| openTelemetryInc | 22.97K | ± 402.02 | ops/s |
| openTelemetryIncNoLabels | 21.80K | ± 383.92 | ops/s |
| openTelemetryAdd | 19.16K | ± 317.73 | ops/s |
| simpleclientInc | 6.53K | ± 90.64 | ops/s |
| simpleclientAdd | 6.38K | ± 94.17 | ops/s |
| simpleclientNoLabelsInc | 6.27K | ± 86.20 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 188.73 | ops/s |
| prometheusClassic | 6.50K | ± 2.01K | ops/s |
| openTelemetryClassic | 5.30K | ± 1.09K | ops/s |
| openTelemetryBoundClassic | 4.83K | ± 1.42K | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 15.46 | ops/s |
| simpleclient | 4.43K | ± 85.16 | ops/s |
| prometheusNative | 2.84K | ± 326.36 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 70.08 | ops/s |
| openTelemetryExponential | 953.51 | ± 50.49 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.42K | ± 656.46 | ops/s |
| prometheusWriteToNull | 22.92K | ± 1.02K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 507.22K | ± 8.34K | ops/s |
| openMetricsWriteToNull | 499.39K | ± 7.71K | ops/s |
| prometheusWriteToByteArray | 498.89K | ± 3.74K | ops/s |
| openMetricsWriteToByteArray | 486.15K | ± 7.76K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.049 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.026 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.073 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.146 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.210 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.888 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.185 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.983 | — | — |
| HistogramBenchmark.prometheusClassic | 0.616 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.667 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.646 | — | — |
| HistogramBenchmark.prometheusNative | 335793.322 | — | — |
| HistogramBenchmark.simpleclient | 0.212 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.151 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.154 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48559.592   ± 2249.447  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19159.754    ± 317.735  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31326.637    ± 794.606  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      36169.105   ± 2926.814  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22967.937    ± 402.023  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21795.922    ± 383.917  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50774.159   ± 1083.533  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  548043845.859 ± 12559975.390  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334791270.625 ± 151177.528  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65394.363   ± 1563.688  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116031354.145 ± 1606087.951  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58512393.579 ± 125907.100  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56131.103   ± 1497.663  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6383.019     ± 94.169  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6534.437     ± 90.640  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6270.639     ± 86.203  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4829.806   ± 1418.652  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1053.886     ± 70.083  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5300.372   ± 1092.461  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        953.506     ± 50.494  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6497.567   ± 2013.872  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11976.479    ± 188.729  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4524.528     ± 15.455  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2837.782    ± 326.358  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.908     ± 85.159  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23418.992    ± 656.457  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22917.553   ± 1019.872  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486146.270   ± 7760.151  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     499394.814   ± 7712.321  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498893.782   ± 3744.852  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507219.165   ± 8339.817  ops/s
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
