# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-19T09:00:36Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 555.27M | ± 8610.65K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.15M | ± 812.71K | ops/s |
| prometheusLabelValuesInc | 115.86M | ± 1749.12K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.42M | ± 186.36K | ops/s |
| prometheusInc | 65.80K | ± 932.84 | ops/s |
| prometheusNoLabelsInc | 56.08K | ± 1.13K | ops/s |
| prometheusAdd | 51.09K | ± 823.26 | ops/s |
| codahaleIncNoLabels | 48.68K | ± 1.28K | ops/s |
| openTelemetryBoundInc | 37.36K | ± 704.14 | ops/s |
| openTelemetryBoundAdd | 32.08K | ± 525.56 | ops/s |
| openTelemetryInc | 23.13K | ± 375.74 | ops/s |
| openTelemetryIncNoLabels | 21.67K | ± 350.02 | ops/s |
| openTelemetryAdd | 19.36K | ± 398.03 | ops/s |
| simpleclientInc | 6.54K | ± 87.72 | ops/s |
| simpleclientNoLabelsInc | 6.26K | ± 112.84 | ops/s |
| simpleclientAdd | 6.09K | ± 250.98 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 192.65 | ops/s |
| prometheusClassic | 6.11K | ± 1.27K | ops/s |
| openTelemetryBoundClassic | 6.01K | ± 145.34 | ops/s |
| prometheusClassicSingleThread | 4.51K | ± 21.31 | ops/s |
| simpleclient | 4.42K | ± 75.54 | ops/s |
| openTelemetryClassic | 3.78K | ± 406.91 | ops/s |
| prometheusNative | 2.73K | ± 232.43 | ops/s |
| openTelemetryBoundExponential | 1.01K | ± 69.77 | ops/s |
| openTelemetryExponential | 958.67 | ± 93.61 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.32K | ± 846.37 | ops/s |
| prometheusWriteToNull | 22.44K | ± 846.94 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 490.32K | ± 4.39K | ops/s |
| prometheusWriteToByteArray | 486.70K | ± 5.91K | ops/s |
| openMetricsWriteToNull | 471.80K | ± 4.00K | ops/s |
| openMetricsWriteToByteArray | 469.90K | ± 3.80K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.048 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.040 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.153 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.156 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.929 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.254 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.985 | — | — |
| HistogramBenchmark.prometheusClassic | 0.630 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.680 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.647 | — | — |
| HistogramBenchmark.prometheusNative | 417713.361 | — | — |
| HistogramBenchmark.simpleclient | 0.214 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.151 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.157 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48680.184   ± 1284.573  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19361.573    ± 398.033  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      32075.615    ± 525.556  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37360.423    ± 704.140  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23132.183    ± 375.739  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21673.793    ± 350.016  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51087.532    ± 823.255  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  555270364.227 ± 8610652.738  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334147855.272 ± 812705.327  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65803.330    ± 932.836  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  115859644.216 ± 1749122.452  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58416945.265 ± 186362.352  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56078.117   ± 1127.774  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6094.454    ± 250.978  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6535.918     ± 87.717  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6262.258    ± 112.842  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6009.573    ± 145.340  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1014.086     ± 69.769  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3777.048    ± 406.913  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        958.666     ± 93.612  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6105.123   ± 1267.687  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11979.019    ± 192.653  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4510.640     ± 21.306  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2732.182    ± 232.430  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.279     ± 75.541  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23316.603    ± 846.373  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22440.408    ± 846.935  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469895.255   ± 3797.665  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     471799.385   ± 4000.849  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486698.400   ± 5912.913  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490319.296   ± 4390.579  ops/s
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
