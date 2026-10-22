# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-22T08:42:37Z
- **Commit:** [`ec63f9b`](https://github.com/dhoard/client_java/commit/ec63f9be83f5f079424be2a29f319f7175f54c9e)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 255.99M | ± 11521.20K | ops/s |
| prometheusLabelValuesInc | 126.20M | ± 852.12K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 95.05M | ± 343.02K | ops/s |
| prometheusLabelValuesIncSingleThread | 62.03M | ± 148.86K | ops/s |
| prometheusInc | 26.99K | ± 731.53 | ops/s |
| codahaleIncNoLabels | 26.88K | ± 425.36 | ops/s |
| prometheusNoLabelsInc | 26.69K | ± 52.99 | ops/s |
| openTelemetryBoundInc | 26.17K | ± 59.25 | ops/s |
| prometheusAdd | 25.79K | ± 103.14 | ops/s |
| openTelemetryBoundAdd | 23.97K | ± 108.30 | ops/s |
| openTelemetryInc | 20.66K | ± 1.07K | ops/s |
| openTelemetryIncNoLabels | 19.92K | ± 802.83 | ops/s |
| openTelemetryAdd | 17.71K | ± 325.09 | ops/s |
| simpleclientInc | 6.72K | ± 45.62 | ops/s |
| simpleclientNoLabelsInc | 6.57K | ± 69.03 | ops/s |
| simpleclientAdd | 6.33K | ± 70.08 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 6.73K | ± 21.61 | ops/s |
| simpleclient | 4.19K | ± 25.18 | ops/s |
| prometheusClassic | 3.70K | ± 116.63 | ops/s |
| openTelemetryClassic | 3.43K | ± 1.94K | ops/s |
| prometheusClassicSingleThread | 2.90K | ± 66.62 | ops/s |
| openTelemetryBoundClassic | 2.89K | ± 129.17 | ops/s |
| prometheusNative | 1.80K | ± 248.50 | ops/s |
| openTelemetryBoundExponential | 686.85 | ± 73.37 | ops/s |
| openTelemetryExponential | 596.16 | ± 54.29 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 18.37K | ± 77.17 | ops/s |
| openMetricsWriteToNull | 18.31K | ± 35.96 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToByteArray | 237.45K | ± 41.22K | ops/s |
| prometheusWriteToByteArray | 222.43K | ± 2.21K | ops/s |
| prometheusWriteToNull | 222.06K | ± 1.32K | ops/s |
| openMetricsWriteToNull | 215.77K | ± 23.63K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.035 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.053 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.036 | — | — |
| CounterBenchmark.openTelemetryInc | 0.046 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.047 | — | — |
| CounterBenchmark.prometheusAdd | 0.143 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.138 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.139 | — | — |
| CounterBenchmark.simpleclientAdd | 0.148 | — | — |
| CounterBenchmark.simpleclientInc | 0.140 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.143 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.333 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.382 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.333 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.593 | — | — |
| HistogramBenchmark.prometheusClassic | 1.002 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 1.204 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.972 | — | — |
| HistogramBenchmark.prometheusNative | 335794.095 | — | — |
| HistogramBenchmark.simpleclient | 0.225 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.193 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.192 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.003 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.003 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.336 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18477.337 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26876.644    ± 425.363  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      17707.042    ± 325.085  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      23972.819    ± 108.299  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      26171.298     ± 59.250  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      20663.388   ± 1068.608  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      19919.082    ± 802.828  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25794.434    ± 103.136  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  255990457.091 ± 11521195.560  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15   95047915.040 ± 343023.847  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26985.188    ± 731.529  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  126203429.488 ± 852121.799  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   62028654.106 ± 148856.464  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26693.511     ± 52.991  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6330.600     ± 70.077  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6723.933     ± 45.623  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6569.444     ± 69.030  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       2892.272    ± 129.169  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        686.853     ± 73.369  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3431.751   ± 1939.929  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        596.164     ± 54.293  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3704.946    ± 116.633  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6732.081     ± 21.607  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2899.921     ± 66.624  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1804.302    ± 248.504  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4188.889     ± 25.176  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18307.913     ± 35.961  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18372.057     ± 77.171  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     237448.681  ± 41223.323  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     215770.642  ± 23627.476  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     222430.866   ± 2212.436  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     222059.100   ± 1321.046  ops/s
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
