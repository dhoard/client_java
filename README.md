# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-15T10:30:18Z
- **Commit:** [`3d95490`](https://github.com/dhoard/client_java/commit/3d95490f7bbccb162de448903e2b737946b8fa59)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 294.75M | ± 7162.67K | ops/s |
| prometheusLabelValuesInc | 93.33M | ± 252.94K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 93.19M | ± 87.21K | ops/s |
| prometheusLabelValuesIncSingleThread | 55.93M | ± 1892.41K | ops/s |
| prometheusInc | 31.31K | ± 77.48 | ops/s |
| prometheusNoLabelsInc | 30.97K | ± 226.53 | ops/s |
| codahaleIncNoLabels | 30.02K | ± 1.10K | ops/s |
| openTelemetryBoundInc | 29.21K | ± 240.39 | ops/s |
| prometheusAdd | 28.29K | ± 117.74 | ops/s |
| openTelemetryBoundAdd | 27.32K | ± 514.77 | ops/s |
| openTelemetryInc | 22.57K | ± 630.84 | ops/s |
| openTelemetryIncNoLabels | 22.00K | ± 1.59K | ops/s |
| openTelemetryAdd | 17.50K | ± 1.18K | ops/s |
| simpleclientInc | 6.52K | ± 289.35 | ops/s |
| simpleclientAdd | 6.17K | ± 238.47 | ops/s |
| simpleclientNoLabelsInc | 6.08K | ± 294.56 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.80K | ± 26.26 | ops/s |
| simpleclient | 4.07K | ± 71.96 | ops/s |
| prometheusClassic | 4.02K | ± 1.93K | ops/s |
| openTelemetryClassic | 3.94K | ± 1.64K | ops/s |
| prometheusClassicSingleThread | 3.23K | ± 78.80 | ops/s |
| openTelemetryBoundClassic | 2.86K | ± 226.94 | ops/s |
| prometheusNative | 2.03K | ± 62.81 | ops/s |
| openTelemetryExponential | 634.71 | ± 83.70 | ops/s |
| openTelemetryBoundExponential | 621.54 | ± 64.56 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 19.83K | ± 109.55 | ops/s |
| openMetricsWriteToNull | 19.71K | ± 143.75 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 331.42K | ± 3.39K | ops/s |
| prometheusWriteToNull | 331.39K | ± 4.95K | ops/s |
| openMetricsWriteToNull | 308.45K | ± 3.00K | ops/s |
| openMetricsWriteToByteArray | 307.68K | ± 1.62K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.031 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.054 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.034 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryInc | 0.042 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.130 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.118 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.119 | — | — |
| CounterBenchmark.simpleclientAdd | 0.152 | — | — |
| CounterBenchmark.simpleclientInc | 0.144 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.154 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.334 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.520 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.267 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.502 | — | — |
| HistogramBenchmark.prometheusClassic | 1.065 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 1.045 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.867 | — | — |
| HistogramBenchmark.prometheusNative | 335793.841 | — | — |
| HistogramBenchmark.simpleclient | 0.232 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.179 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.178 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.669 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18466.669 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30015.069   ± 1095.208  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      17497.336   ± 1175.972  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      27321.903    ± 514.765  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      29209.187    ± 240.386  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22566.351    ± 630.841  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21998.968   ± 1592.619  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28290.542    ± 117.736  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  294748841.020 ± 7162666.231  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15   93194278.683  ± 87208.631  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31313.822     ± 77.483  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15   93334342.240 ± 252937.032  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   55930516.076 ± 1892412.317  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30967.194    ± 226.533  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6165.840    ± 238.471  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6522.535    ± 289.350  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6078.442    ± 294.557  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       2856.544    ± 226.937  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        621.544     ± 64.562  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3943.083   ± 1639.557  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        634.713     ± 83.702  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4020.349   ± 1931.185  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7803.409     ± 26.259  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3225.693     ± 78.796  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2025.474     ± 62.811  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4072.956     ± 71.956  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      19711.688    ± 143.750  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19832.719    ± 109.548  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     307684.388   ± 1616.359  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     308445.535   ± 2999.249  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     331418.463   ± 3389.038  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     331386.540   ± 4953.085  ops/s
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
