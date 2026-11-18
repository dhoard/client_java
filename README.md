# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-18T11:19:36Z
- **Commit:** [`3ea508f`](https://github.com/dhoard/client_java/commit/3ea508f61ddaa1f8b43266e3bf378d7f60e14f25)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 657.64M | ± 69801.62K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 210.09M | ± 1157.62K | ops/s |
| prometheusLabelValuesInc | 197.73M | ± 2630.74K | ops/s |
| prometheusLabelValuesIncSingleThread | 94.43M | ± 2297.32K | ops/s |
| prometheusInc | 65.47K | ± 270.70 | ops/s |
| prometheusNoLabelsInc | 64.14K | ± 488.76 | ops/s |
| codahaleIncNoLabels | 61.12K | ± 617.28 | ops/s |
| prometheusAdd | 58.82K | ± 2.48K | ops/s |
| openTelemetryBoundInc | 53.37K | ± 512.06 | ops/s |
| openTelemetryBoundAdd | 46.57K | ± 333.74 | ops/s |
| openTelemetryIncNoLabels | 35.46K | ± 978.14 | ops/s |
| openTelemetryInc | 35.44K | ± 743.74 | ops/s |
| openTelemetryAdd | 28.31K | ± 1.17K | ops/s |
| simpleclientNoLabelsInc | 10.56K | ± 120.65 | ops/s |
| simpleclientInc | 10.52K | ± 244.66 | ops/s |
| simpleclientAdd | 10.06K | ± 31.22 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.10K | ± 203.14 | ops/s |
| prometheusClassic | 9.67K | ± 971.94 | ops/s |
| simpleclient | 7.05K | ± 105.24 | ops/s |
| openTelemetryClassic | 4.91K | ± 146.94 | ops/s |
| prometheusClassicSingleThread | 4.44K | ± 96.02 | ops/s |
| openTelemetryBoundClassic | 4.36K | ± 329.28 | ops/s |
| prometheusNative | 4.16K | ± 714.05 | ops/s |
| openTelemetryBoundExponential | 1.12K | ± 47.75 | ops/s |
| openTelemetryExponential | 1.02K | ± 28.75 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 36.10K | ± 622.35 | ops/s |
| openMetricsWriteToNull | 35.45K | ± 512.62 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 839.26K | ± 54.33K | ops/s |
| prometheusWriteToNull | 811.99K | ± 47.26K | ops/s |
| openMetricsWriteToByteArray | 751.81K | ± 37.55K | ops/s |
| openMetricsWriteToNull | 706.35K | ± 19.62K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.033 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.027 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.027 | — | — |
| CounterBenchmark.prometheusAdd | 0.063 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.058 | — | — |
| CounterBenchmark.simpleclientAdd | 0.094 | — | — |
| CounterBenchmark.simpleclientInc | 0.090 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.090 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.218 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.846 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.194 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.929 | — | — |
| HistogramBenchmark.prometheusClassic | 0.385 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.539 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.617 | — | — |
| HistogramBenchmark.prometheusNative | 417712.922 | — | — |
| HistogramBenchmark.simpleclient | 0.134 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.099 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.098 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18477.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61117.227    ± 617.284  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      28311.391   ± 1169.181  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      46569.009    ± 333.736  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      53366.058    ± 512.062  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      35435.560    ± 743.743  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      35457.869    ± 978.139  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58818.789   ± 2476.649  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  657636849.108 ± 69801617.626  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  210088713.339 ± 1157621.510  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65466.254    ± 270.703  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  197731148.401 ± 2630742.979  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   94427790.948 ± 2297320.536  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64141.852    ± 488.764  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10063.767     ± 31.224  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10520.619    ± 244.664  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10561.689    ± 120.649  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4361.058    ± 329.279  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1118.696     ± 47.753  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4911.644    ± 146.941  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1019.192     ± 28.747  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9671.806    ± 971.943  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15102.712    ± 203.141  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4436.386     ± 96.023  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4157.885    ± 714.053  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7051.097    ± 105.243  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35454.038    ± 512.617  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      36102.070    ± 622.355  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     751808.697  ± 37546.590  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     706346.528  ± 19620.002  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     839260.292  ± 54329.151  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     811988.264  ± 47257.232  ops/s
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
