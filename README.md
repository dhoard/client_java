# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-05T10:37:37Z
- **Commit:** [`7911c52`](https://github.com/dhoard/client_java/commit/7911c52e92b69b379bedc02d19a11c09d484eb64)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 555.27M | ± 11733.41K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.46M | ± 252.92K | ops/s |
| prometheusLabelValuesInc | 115.51M | ± 2173.41K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.42M | ± 267.41K | ops/s |
| prometheusInc | 66.22K | ± 1.28K | ops/s |
| prometheusNoLabelsInc | 56.63K | ± 773.57 | ops/s |
| prometheusAdd | 50.78K | ± 1.08K | ops/s |
| codahaleIncNoLabels | 48.40K | ± 3.34K | ops/s |
| openTelemetryBoundInc | 37.51K | ± 639.61 | ops/s |
| openTelemetryBoundAdd | 31.81K | ± 590.89 | ops/s |
| openTelemetryInc | 23.23K | ± 392.89 | ops/s |
| openTelemetryIncNoLabels | 21.70K | ± 345.81 | ops/s |
| openTelemetryAdd | 19.31K | ± 270.49 | ops/s |
| simpleclientInc | 6.53K | ± 96.16 | ops/s |
| simpleclientNoLabelsInc | 6.34K | ± 124.55 | ops/s |
| simpleclientAdd | 6.13K | ± 250.74 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.97K | ± 171.68 | ops/s |
| prometheusClassic | 5.69K | ± 985.63 | ops/s |
| openTelemetryClassic | 4.71K | ± 1.17K | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 18.37 | ops/s |
| simpleclient | 4.40K | ± 80.68 | ops/s |
| openTelemetryBoundClassic | 3.87K | ± 1.10K | ops/s |
| prometheusNative | 2.98K | ± 107.18 | ops/s |
| openTelemetryBoundExponential | 1.04K | ± 17.51 | ops/s |
| openTelemetryExponential | 894.00 | ± 108.71 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.42K | ± 989.45 | ops/s |
| prometheusWriteToNull | 30.11K | ± 1.37K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 499.27K | ± 3.57K | ops/s |
| prometheusWriteToByteArray | 489.74K | ± 12.17K | ops/s |
| openMetricsWriteToNull | 487.66K | ± 4.51K | ops/s |
| openMetricsWriteToByteArray | 478.45K | ± 5.24K | ops/s |

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
| CounterBenchmark.prometheusAdd | 0.073 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.153 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.147 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.258 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.908 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.207 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.061 | — | — |
| HistogramBenchmark.prometheusClassic | 0.669 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.682 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.646 | — | — |
| HistogramBenchmark.prometheusNative | 335793.250 | — | — |
| HistogramBenchmark.simpleclient | 0.213 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.116 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.117 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18496.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48395.666   ± 3341.534  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19313.574    ± 270.490  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31806.872    ± 590.887  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37511.486    ± 639.612  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23227.524    ± 392.890  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21697.062    ± 345.812  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50775.876   ± 1075.811  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  555271371.423 ± 11733410.263  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334463806.523 ± 252922.682  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66220.958   ± 1281.222  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  115513266.553 ± 2173410.955  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58422726.733 ± 267405.024  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56630.886    ± 773.570  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6130.670    ± 250.735  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.584     ± 96.159  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6344.064    ± 124.552  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       3874.104   ± 1100.870  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1035.420     ± 17.515  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4713.127   ± 1165.988  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        893.998    ± 108.709  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5686.391    ± 985.626  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11969.961    ± 171.676  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4519.763     ± 18.368  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2982.686    ± 107.179  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.792     ± 80.683  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30419.297    ± 989.454  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      30111.845   ± 1369.443  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478446.494   ± 5240.050  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487655.239   ± 4511.628  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489741.993  ± 12167.326  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499266.958   ± 3567.650  ops/s
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
