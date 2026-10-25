# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-25T09:00:57Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 550.83M | ± 8507.57K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.60M | ± 311.72K | ops/s |
| prometheusLabelValuesInc | 116.12M | ± 1967.18K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.42M | ± 297.64K | ops/s |
| prometheusInc | 65.77K | ± 952.31 | ops/s |
| prometheusNoLabelsInc | 56.18K | ± 814.11 | ops/s |
| prometheusAdd | 50.31K | ± 1.59K | ops/s |
| codahaleIncNoLabels | 48.08K | ± 1.56K | ops/s |
| openTelemetryBoundInc | 37.79K | ± 594.53 | ops/s |
| openTelemetryBoundAdd | 31.22K | ± 613.19 | ops/s |
| openTelemetryInc | 23.16K | ± 291.75 | ops/s |
| openTelemetryIncNoLabels | 22.57K | ± 1.17K | ops/s |
| openTelemetryAdd | 19.34K | ± 344.07 | ops/s |
| simpleclientInc | 6.56K | ± 93.87 | ops/s |
| simpleclientNoLabelsInc | 6.30K | ± 210.81 | ops/s |
| simpleclientAdd | 6.29K | ± 206.91 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.97K | ± 188.33 | ops/s |
| prometheusClassic | 7.40K | ± 1.53K | ops/s |
| openTelemetryClassic | 4.75K | ± 552.02 | ops/s |
| openTelemetryBoundClassic | 4.59K | ± 1.86K | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 15.27 | ops/s |
| simpleclient | 4.41K | ± 73.30 | ops/s |
| prometheusNative | 2.84K | ± 219.96 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 88.66 | ops/s |
| openTelemetryExponential | 962.85 | ± 41.45 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.54K | ± 1.06K | ops/s |
| prometheusWriteToNull | 29.52K | ± 415.05 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 512.88K | ± 1.58K | ops/s |
| openMetricsWriteToNull | 504.81K | ± 7.50K | ops/s |
| prometheusWriteToByteArray | 503.75K | ± 5.88K | ops/s |
| openMetricsWriteToByteArray | 489.74K | ± 7.66K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.020 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.048 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.040 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.042 | — | — |
| CounterBenchmark.prometheusAdd | 0.074 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.149 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.148 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.237 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.891 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.201 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.974 | — | — |
| HistogramBenchmark.prometheusClassic | 0.515 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.673 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.645 | — | — |
| HistogramBenchmark.prometheusNative | 417713.311 | — | — |
| HistogramBenchmark.simpleclient | 0.212 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.115 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.119 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48081.302   ± 1564.194  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19337.424    ± 344.074  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31216.660    ± 613.193  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37793.585    ± 594.533  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23159.147    ± 291.751  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22570.065   ± 1166.120  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50311.906   ± 1593.577  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  550827787.595 ± 8507570.488  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334596046.863 ± 311716.487  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65771.262    ± 952.314  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116120874.312 ± 1967179.679  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58421777.437 ± 297638.448  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56182.008    ± 814.113  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6288.627    ± 206.914  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6558.828     ± 93.869  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6303.357    ± 210.805  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4587.672   ± 1860.013  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1053.928     ± 88.655  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4750.459    ± 552.024  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        962.847     ± 41.451  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7399.197   ± 1526.070  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11967.373    ± 188.331  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4524.518     ± 15.267  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2837.055    ± 219.959  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.659     ± 73.299  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30538.604   ± 1061.460  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      29522.686    ± 415.053  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489737.552   ± 7664.879  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     504805.797   ± 7495.631  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503753.125   ± 5883.909  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512876.074   ± 1581.893  ops/s
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
