# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-06T10:37:18Z
- **Commit:** [`7911c52`](https://github.com/dhoard/client_java/commit/7911c52e92b69b379bedc02d19a11c09d484eb64)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 680.76M | ± 1685.19K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.40M | ± 418.33K | ops/s |
| prometheusLabelValuesInc | 138.57M | ± 2744.83K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.18M | ± 351.96K | ops/s |
| prometheusInc | 76.80K | ± 575.68 | ops/s |
| prometheusNoLabelsInc | 65.96K | ± 750.52 | ops/s |
| prometheusAdd | 62.27K | ± 397.74 | ops/s |
| codahaleIncNoLabels | 57.06K | ± 515.05 | ops/s |
| openTelemetryBoundInc | 45.63K | ± 112.64 | ops/s |
| openTelemetryBoundAdd | 38.44K | ± 278.15 | ops/s |
| openTelemetryInc | 27.59K | ± 196.43 | ops/s |
| openTelemetryIncNoLabels | 26.93K | ± 201.23 | ops/s |
| openTelemetryAdd | 24.10K | ± 43.84 | ops/s |
| simpleclientInc | 7.94K | ± 21.68 | ops/s |
| simpleclientNoLabelsInc | 7.67K | ± 184.61 | ops/s |
| simpleclientAdd | 7.49K | ± 357.02 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.39K | ± 142.72 | ops/s |
| prometheusClassic | 9.19K | ± 189.24 | ops/s |
| prometheusClassicSingleThread | 7.10K | ± 240.87 | ops/s |
| openTelemetryClassic | 6.83K | ± 1.51K | ops/s |
| openTelemetryBoundClassic | 6.72K | ± 1.21K | ops/s |
| simpleclient | 5.77K | ± 108.12 | ops/s |
| prometheusNative | 3.37K | ± 89.98 | ops/s |
| openTelemetryBoundExponential | 907.11 | ± 44.83 | ops/s |
| openTelemetryExponential | 860.80 | ± 43.76 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.59K | ± 382.40 | ops/s |
| openMetricsWriteToNull | 40.54K | ± 348.17 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 772.78K | ± 6.68K | ops/s |
| prometheusWriteToByteArray | 751.73K | ± 9.55K | ops/s |
| openMetricsWriteToNull | 719.60K | ± 10.76K | ops/s |
| openMetricsWriteToByteArray | 709.24K | ± 12.01K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.024 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.021 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.035 | — | — |
| CounterBenchmark.prometheusAdd | 0.059 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.126 | — | — |
| CounterBenchmark.simpleclientInc | 0.118 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.123 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.144 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.040 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.145 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.097 | — | — |
| HistogramBenchmark.prometheusClassic | 0.402 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.465 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.412 | — | — |
| HistogramBenchmark.prometheusNative | 253873.103 | — | — |
| HistogramBenchmark.simpleclient | 0.164 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.087 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57064.590    ± 515.053  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24099.338     ± 43.839  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38435.582    ± 278.149  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      45629.946    ± 112.640  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27586.011    ± 196.434  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      26926.705    ± 201.233  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62272.780    ± 397.737  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  680756055.026 ± 1685190.868  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370404747.088 ± 418329.193  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76804.188    ± 575.683  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  138568098.920 ± 2744826.641  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68176757.543 ± 351961.354  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65961.037    ± 750.521  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7485.114    ± 357.019  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7942.855     ± 21.682  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7668.348    ± 184.611  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6722.645   ± 1211.544  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        907.114     ± 44.830  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6827.384   ± 1508.043  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        860.801     ± 43.763  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9187.579    ± 189.235  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17392.597    ± 142.719  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7102.551    ± 240.875  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3372.366     ± 89.977  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5765.478    ± 108.119  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40540.613    ± 348.174  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40586.105    ± 382.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     709236.191  ± 12006.380  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     719595.927  ± 10760.270  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     751729.361   ± 9549.232  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     772781.943   ± 6680.126  ops/s
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
