# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-28T09:36:12Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 549.67M | ± 12690.10K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.39M | ± 249.27K | ops/s |
| prometheusLabelValuesInc | 114.49M | ± 1803.39K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.48M | ± 128.92K | ops/s |
| prometheusInc | 65.88K | ± 798.59 | ops/s |
| prometheusNoLabelsInc | 55.60K | ± 1.10K | ops/s |
| prometheusAdd | 51.06K | ± 877.76 | ops/s |
| codahaleIncNoLabels | 48.75K | ± 1.83K | ops/s |
| openTelemetryBoundInc | 37.53K | ± 638.64 | ops/s |
| openTelemetryBoundAdd | 31.87K | ± 644.72 | ops/s |
| openTelemetryInc | 23.07K | ± 436.85 | ops/s |
| openTelemetryIncNoLabels | 21.87K | ± 370.20 | ops/s |
| openTelemetryAdd | 18.78K | ± 809.21 | ops/s |
| simpleclientInc | 6.52K | ± 89.16 | ops/s |
| simpleclientAdd | 6.29K | ± 232.32 | ops/s |
| simpleclientNoLabelsInc | 6.26K | ± 99.40 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 192.84 | ops/s |
| prometheusClassic | 5.91K | ± 1.44K | ops/s |
| openTelemetryBoundClassic | 5.71K | ± 1.78K | ops/s |
| prometheusClassicSingleThread | 4.51K | ± 30.79 | ops/s |
| openTelemetryClassic | 4.46K | ± 1.21K | ops/s |
| simpleclient | 4.42K | ± 77.91 | ops/s |
| prometheusNative | 2.78K | ± 333.06 | ops/s |
| openTelemetryBoundExponential | 1.07K | ± 16.93 | ops/s |
| openTelemetryExponential | 938.13 | ± 87.33 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.12K | ± 641.93 | ops/s |
| prometheusWriteToNull | 30.08K | ± 1.84K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 509.73K | ± 3.24K | ops/s |
| prometheusWriteToNull | 508.23K | ± 5.77K | ops/s |
| openMetricsWriteToNull | 494.57K | ± 4.41K | ops/s |
| openMetricsWriteToByteArray | 489.80K | ± 4.78K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.050 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.149 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.177 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.875 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.221 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.003 | — | — |
| HistogramBenchmark.prometheusClassic | 0.658 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.665 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.648 | — | — |
| HistogramBenchmark.prometheusNative | 402682.813 | — | — |
| HistogramBenchmark.simpleclient | 0.213 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.117 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.117 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18442.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48746.405   ± 1832.133  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      18784.562    ± 809.211  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31873.946    ± 644.722  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37527.202    ± 638.638  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23068.480    ± 436.848  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21873.649    ± 370.202  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51059.471    ± 877.763  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  549669676.815 ± 12690101.497  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334389556.220 ± 249268.205  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65877.842    ± 798.593  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  114488692.552 ± 1803386.392  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58481305.982 ± 128918.263  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55601.383   ± 1096.053  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6287.308    ± 232.318  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6518.152     ± 89.155  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6263.023     ± 99.397  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5712.817   ± 1779.922  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1069.019     ± 16.930  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4457.226   ± 1210.137  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        938.126     ± 87.328  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5908.728   ± 1439.615  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11975.403    ± 192.840  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4507.394     ± 30.785  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2779.181    ± 333.061  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.844     ± 77.913  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30120.104    ± 641.925  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      30081.345   ± 1836.826  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489802.577   ± 4780.937  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     494573.655   ± 4405.515  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509733.540   ± 3235.436  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508234.014   ± 5765.437  ops/s
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
