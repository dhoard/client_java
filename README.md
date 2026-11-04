# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-04T10:10:54Z
- **Commit:** [`7911c52`](https://github.com/dhoard/client_java/commit/7911c52e92b69b379bedc02d19a11c09d484eb64)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** Intel(R) Xeon(R) 6975P-C, 4 cores, 15 GB RAM
- **OS:** Linux 7.0.0-1014-aws

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 332.15M | ± 3659.76K | ops/s |
| prometheusLabelValuesInc | 173.19M | ± 986.36K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 123.49M | ± 211.04K | ops/s |
| prometheusLabelValuesIncSingleThread | 83.08M | ± 190.81K | ops/s |
| prometheusAdd | 33.90K | ± 378.01 | ops/s |
| openTelemetryBoundInc | 33.52K | ± 1.17K | ops/s |
| codahaleIncNoLabels | 33.28K | ± 2.41K | ops/s |
| prometheusInc | 32.92K | ± 156.50 | ops/s |
| prometheusNoLabelsInc | 32.71K | ± 1.31K | ops/s |
| openTelemetryBoundAdd | 31.68K | ± 1.64K | ops/s |
| openTelemetryIncNoLabels | 29.58K | ± 399.81 | ops/s |
| openTelemetryInc | 29.10K | ± 637.93 | ops/s |
| openTelemetryAdd | 25.54K | ± 146.88 | ops/s |
| simpleclientAdd | 7.56K | ± 52.56 | ops/s |
| simpleclientInc | 7.54K | ± 93.74 | ops/s |
| simpleclientNoLabelsInc | 7.52K | ± 40.84 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 8.46K | ± 11.50 | ops/s |
| simpleclient | 5.23K | ± 37.10 | ops/s |
| prometheusClassicSingleThread | 4.22K | ± 13.18 | ops/s |
| prometheusClassic | 4.11K | ± 1.76K | ops/s |
| openTelemetryBoundClassic | 3.82K | ± 3.29K | ops/s |
| openTelemetryClassic | 2.42K | ± 238.67 | ops/s |
| prometheusNative | 2.39K | ± 290.96 | ops/s |
| openTelemetryExponential | 362.81 | ± 10.65 | ops/s |
| openTelemetryBoundExponential | 358.90 | ± 20.47 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 25.78K | ± 43.65 | ops/s |
| openMetricsWriteToNull | 25.75K | ± 46.41 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 446.64K | ± 2.74K | ops/s |
| prometheusWriteToNull | 444.30K | ± 3.26K | ops/s |
| openMetricsWriteToNull | 415.85K | ± 1.32K | ops/s |
| openMetricsWriteToByteArray | 414.26K | ± 3.01K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.028 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.037 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.028 | — | — |
| CounterBenchmark.openTelemetryInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.032 | — | — |
| CounterBenchmark.prometheusAdd | 0.111 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.114 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.116 | — | — |
| CounterBenchmark.simpleclientAdd | 0.125 | — | — |
| CounterBenchmark.simpleclientInc | 0.125 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.125 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.386 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 2.638 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.396 | — | — |
| HistogramBenchmark.openTelemetryExponential | 2.606 | — | — |
| HistogramBenchmark.prometheusClassic | 1.051 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.965 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.656 | — | — |
| HistogramBenchmark.prometheusNative | 417713.582 | — | — |
| HistogramBenchmark.simpleclient | 0.181 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.137 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.137 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.002 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      33275.748   ± 2409.251  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      25535.135    ± 146.877  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31680.878   ± 1638.928  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      33520.349   ± 1168.900  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      29102.956    ± 637.931  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      29575.621    ± 399.812  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      33895.852    ± 378.005  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  332147892.663 ± 3659756.756  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  123488553.926 ± 211036.555  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      32916.744    ± 156.501  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  173190673.068 ± 986364.828  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   83083476.263 ± 190808.136  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      32710.081   ± 1310.115  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7561.143     ± 52.558  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7544.246     ± 93.738  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7519.912     ± 40.841  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       3817.520   ± 3292.065  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        358.901     ± 20.472  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       2417.718    ± 238.672  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        362.808     ± 10.652  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4110.248   ± 1763.389  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       8457.152     ± 11.502  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4215.752     ± 13.179  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2385.689    ± 290.957  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5232.731     ± 37.097  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      25752.505     ± 46.409  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      25784.864     ± 43.649  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     414261.216   ± 3014.124  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     415852.227   ± 1323.116  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     446639.468   ± 2739.293  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     444304.709   ± 3256.790  ops/s
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
