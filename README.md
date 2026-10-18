# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-18T08:41:10Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 678.11M | ± 54533.41K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 212.88M | ± 2528.75K | ops/s |
| prometheusLabelValuesInc | 200.99M | ± 1150.02K | ops/s |
| prometheusLabelValuesIncSingleThread | 93.85M | ± 878.78K | ops/s |
| prometheusInc | 66.33K | ± 630.97 | ops/s |
| prometheusNoLabelsInc | 65.51K | ± 1.30K | ops/s |
| codahaleIncNoLabels | 61.32K | ± 569.26 | ops/s |
| prometheusAdd | 56.53K | ± 678.48 | ops/s |
| openTelemetryBoundInc | 52.24K | ± 635.98 | ops/s |
| openTelemetryBoundAdd | 47.79K | ± 605.25 | ops/s |
| openTelemetryIncNoLabels | 35.30K | ± 866.91 | ops/s |
| openTelemetryInc | 33.43K | ± 1.62K | ops/s |
| openTelemetryAdd | 28.34K | ± 2.33K | ops/s |
| simpleclientInc | 11.05K | ± 155.31 | ops/s |
| simpleclientNoLabelsInc | 10.70K | ± 204.94 | ops/s |
| simpleclientAdd | 10.13K | ± 96.78 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.77K | ± 241.63 | ops/s |
| prometheusClassic | 8.71K | ± 1.85K | ops/s |
| simpleclient | 7.03K | ± 137.37 | ops/s |
| openTelemetryBoundClassic | 6.50K | ± 2.29K | ops/s |
| openTelemetryClassic | 5.06K | ± 224.60 | ops/s |
| prometheusNative | 4.63K | ± 348.90 | ops/s |
| prometheusClassicSingleThread | 4.34K | ± 35.91 | ops/s |
| openTelemetryBoundExponential | 1.10K | ± 26.72 | ops/s |
| openTelemetryExponential | 1.05K | ± 22.57 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 32.41K | ± 398.24 | ops/s |
| prometheusWriteToNull | 32.21K | ± 415.11 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 857.89K | ± 18.81K | ops/s |
| prometheusWriteToByteArray | 827.68K | ± 23.70K | ops/s |
| openMetricsWriteToNull | 714.48K | ± 56.61K | ops/s |
| openMetricsWriteToByteArray | 670.15K | ± 15.16K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.034 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.028 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.027 | — | — |
| CounterBenchmark.prometheusAdd | 0.066 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.093 | — | — |
| CounterBenchmark.simpleclientInc | 0.085 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.088 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.159 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.862 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.189 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.900 | — | — |
| HistogramBenchmark.prometheusClassic | 0.444 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.537 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.650 | — | — |
| HistogramBenchmark.prometheusNative | 417712.825 | — | — |
| HistogramBenchmark.simpleclient | 0.135 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.109 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.109 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61316.574    ± 569.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      28339.731   ± 2328.357  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      47791.683    ± 605.249  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      52239.660    ± 635.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      33427.460   ± 1624.587  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      35301.774    ± 866.910  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56534.227    ± 678.479  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  678105108.712 ± 54533407.874  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  212878000.669 ± 2528749.837  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66328.258    ± 630.972  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  200987820.062 ± 1150017.600  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   93847518.962 ± 878776.265  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65509.692   ± 1304.495  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10134.782     ± 96.783  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11045.250    ± 155.310  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10701.228    ± 204.941  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6496.994   ± 2289.344  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1098.871     ± 26.718  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5062.880    ± 224.599  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1054.756     ± 22.567  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8713.179   ± 1847.389  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14766.237    ± 241.630  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4340.529     ± 35.913  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4630.424    ± 348.903  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7026.831    ± 137.374  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32414.814    ± 398.236  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32211.746    ± 415.107  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     670149.744  ± 15159.701  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     714480.532  ± 56611.274  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     827683.862  ± 23702.090  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     857886.250  ± 18809.065  ops/s
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
