# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-31T09:37:10Z
- **Commit:** [`e574d32`](https://github.com/dhoard/client_java/commit/e574d3226951fbecda109554024dc1f99eb8d5d5)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 548.33M | ± 9940.41K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 333.79M | ± 788.48K | ops/s |
| prometheusLabelValuesInc | 114.52M | ± 1959.30K | ops/s |
| prometheusLabelValuesIncSingleThread | 57.93M | ± 928.83K | ops/s |
| prometheusInc | 64.59K | ± 1.53K | ops/s |
| prometheusNoLabelsInc | 56.68K | ± 992.85 | ops/s |
| prometheusAdd | 51.39K | ± 726.53 | ops/s |
| codahaleIncNoLabels | 48.86K | ± 1.69K | ops/s |
| openTelemetryBoundInc | 37.77K | ± 528.01 | ops/s |
| openTelemetryBoundAdd | 31.53K | ± 726.51 | ops/s |
| openTelemetryInc | 23.10K | ± 343.73 | ops/s |
| openTelemetryIncNoLabels | 23.07K | ± 1.51K | ops/s |
| openTelemetryAdd | 19.19K | ± 268.75 | ops/s |
| simpleclientInc | 6.53K | ± 132.21 | ops/s |
| simpleclientNoLabelsInc | 6.26K | ± 106.50 | ops/s |
| simpleclientAdd | 6.20K | ± 173.50 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.00K | ± 162.12 | ops/s |
| prometheusClassic | 5.51K | ± 1.67K | ops/s |
| openTelemetryClassic | 4.56K | ± 1.15K | ops/s |
| prometheusClassicSingleThread | 4.53K | ± 15.47 | ops/s |
| simpleclient | 4.34K | ± 174.26 | ops/s |
| openTelemetryBoundClassic | 3.36K | ± 944.77 | ops/s |
| prometheusNative | 2.46K | ± 422.86 | ops/s |
| openTelemetryBoundExponential | 1.06K | ± 35.25 | ops/s |
| openTelemetryExponential | 974.68 | ± 39.42 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 31.73K | ± 964.10 | ops/s |
| openMetricsWriteToNull | 29.65K | ± 956.41 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 508.04K | ± 5.03K | ops/s |
| prometheusWriteToByteArray | 501.57K | ± 3.79K | ops/s |
| openMetricsWriteToNull | 491.59K | ± 4.06K | ops/s |
| openMetricsWriteToByteArray | 489.41K | ± 7.08K | ops/s |

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
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.150 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.302 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.886 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.214 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.961 | — | — |
| HistogramBenchmark.prometheusClassic | 0.720 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.673 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.644 | — | — |
| HistogramBenchmark.prometheusNative | 417713.536 | — | — |
| HistogramBenchmark.simpleclient | 0.218 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.119 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.111 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18477.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48864.584   ± 1689.718  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19188.513    ± 268.753  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31525.526    ± 726.505  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37768.643    ± 528.007  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23095.404    ± 343.730  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      23066.491   ± 1509.175  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51392.913    ± 726.532  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  548333643.523 ± 9940410.908  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  333785122.261 ± 788475.078  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64590.961   ± 1526.917  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  114524442.454 ± 1959301.935  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   57929139.478 ± 928831.839  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56677.049    ± 992.850  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6197.343    ± 173.496  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.726    ± 132.212  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6260.060    ± 106.497  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       3363.969    ± 944.774  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1059.580     ± 35.251  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4556.364   ± 1151.764  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        974.682     ± 39.419  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5513.656   ± 1668.906  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12003.016    ± 162.123  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4527.633     ± 15.472  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2456.017    ± 422.856  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4344.345    ± 174.260  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      29645.683    ± 956.407  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      31725.619    ± 964.099  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489414.975   ± 7081.656  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491591.042   ± 4058.902  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     501573.100   ± 3793.664  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508042.264   ± 5032.070  ops/s
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
