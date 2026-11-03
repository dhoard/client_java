# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-03T10:41:51Z
- **Commit:** [`7911c52`](https://github.com/dhoard/client_java/commit/7911c52e92b69b379bedc02d19a11c09d484eb64)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 685.36M | ± 29187.96K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.69M | ± 394.74K | ops/s |
| prometheusLabelValuesInc | 142.72M | ± 1750.17K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.21M | ± 476.35K | ops/s |
| prometheusInc | 77.53K | ± 1.28K | ops/s |
| prometheusNoLabelsInc | 66.65K | ± 1.05K | ops/s |
| prometheusAdd | 61.50K | ± 826.36 | ops/s |
| codahaleIncNoLabels | 56.86K | ± 557.60 | ops/s |
| openTelemetryBoundInc | 42.64K | ± 2.21K | ops/s |
| openTelemetryBoundAdd | 38.78K | ± 484.67 | ops/s |
| openTelemetryInc | 27.55K | ± 217.39 | ops/s |
| openTelemetryIncNoLabels | 26.83K | ± 1.26K | ops/s |
| openTelemetryAdd | 24.34K | ± 466.93 | ops/s |
| simpleclientInc | 7.80K | ± 166.45 | ops/s |
| simpleclientNoLabelsInc | 7.57K | ± 27.98 | ops/s |
| simpleclientAdd | 7.20K | ± 384.97 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.51K | ± 49.19 | ops/s |
| prometheusClassic | 7.76K | ± 2.93K | ops/s |
| prometheusClassicSingleThread | 7.21K | ± 21.87 | ops/s |
| openTelemetryClassic | 6.21K | ± 1.55K | ops/s |
| simpleclient | 5.70K | ± 169.08 | ops/s |
| openTelemetryBoundClassic | 5.39K | ± 261.30 | ops/s |
| prometheusNative | 3.40K | ± 150.09 | ops/s |
| openTelemetryBoundExponential | 996.88 | ± 65.94 | ops/s |
| openTelemetryExponential | 888.49 | ± 62.42 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.97K | ± 285.12 | ops/s |
| openMetricsWriteToNull | 40.72K | ± 322.49 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 778.27K | ± 6.13K | ops/s |
| prometheusWriteToByteArray | 761.31K | ± 9.09K | ops/s |
| openMetricsWriteToNull | 727.02K | ± 11.99K | ops/s |
| openMetricsWriteToByteArray | 708.72K | ± 13.74K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.017 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.024 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.022 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.035 | — | — |
| CounterBenchmark.prometheusAdd | 0.060 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.131 | — | — |
| CounterBenchmark.simpleclientInc | 0.120 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.125 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.174 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.950 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.159 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.065 | — | — |
| HistogramBenchmark.prometheusClassic | 0.529 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.463 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.405 | — | — |
| HistogramBenchmark.prometheusNative | 417713.092 | — | — |
| HistogramBenchmark.simpleclient | 0.165 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.086 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56862.686    ± 557.598  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24339.781    ± 466.930  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38783.668    ± 484.675  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      42640.698   ± 2211.499  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27552.989    ± 217.387  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      26827.110   ± 1259.391  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61495.812    ± 826.361  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  685363020.156 ± 29187959.695  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370690214.513 ± 394738.258  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77530.819   ± 1277.003  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  142724670.262 ± 1750170.172  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68206748.080 ± 476353.688  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66649.161   ± 1054.118  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7202.089    ± 384.971  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7796.405    ± 166.455  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7565.076     ± 27.976  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5391.921    ± 261.299  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        996.877     ± 65.943  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6213.513   ± 1546.100  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        888.494     ± 62.423  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7761.364   ± 2926.950  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17510.714     ± 49.188  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7214.081     ± 21.865  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3396.866    ± 150.090  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5702.604    ± 169.083  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40715.260    ± 322.491  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40969.638    ± 285.124  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     708720.095  ± 13744.217  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     727015.765  ± 11990.088  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     761307.149   ± 9086.193  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     778272.059   ± 6125.581  ops/s
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
