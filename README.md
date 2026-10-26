# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-26T09:07:47Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 543.27M | ± 17010.51K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.02M | ± 616.21K | ops/s |
| prometheusLabelValuesInc | 113.81M | ± 1957.20K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.07M | ± 404.53K | ops/s |
| prometheusInc | 64.16K | ± 2.18K | ops/s |
| prometheusNoLabelsInc | 55.43K | ± 1.26K | ops/s |
| prometheusAdd | 51.03K | ± 881.96 | ops/s |
| codahaleIncNoLabels | 50.27K | ± 726.62 | ops/s |
| openTelemetryBoundInc | 38.00K | ± 686.14 | ops/s |
| openTelemetryBoundAdd | 31.96K | ± 595.35 | ops/s |
| openTelemetryInc | 23.14K | ± 422.85 | ops/s |
| openTelemetryIncNoLabels | 21.80K | ± 387.26 | ops/s |
| openTelemetryAdd | 17.54K | ± 2.57K | ops/s |
| simpleclientInc | 6.53K | ± 101.52 | ops/s |
| simpleclientAdd | 6.37K | ± 119.81 | ops/s |
| simpleclientNoLabelsInc | 6.28K | ± 90.64 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.98K | ± 191.07 | ops/s |
| prometheusClassic | 6.28K | ± 2.32K | ops/s |
| openTelemetryBoundClassic | 5.47K | ± 1.47K | ops/s |
| openTelemetryClassic | 4.70K | ± 730.19 | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 24.15 | ops/s |
| simpleclient | 4.39K | ± 71.82 | ops/s |
| prometheusNative | 2.76K | ± 197.80 | ops/s |
| openTelemetryBoundExponential | 1.04K | ± 46.24 | ops/s |
| openTelemetryExponential | 998.62 | ± 26.15 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.59K | ± 1.58K | ops/s |
| prometheusWriteToNull | 30.20K | ± 364.07 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 495.69K | ± 4.80K | ops/s |
| prometheusWriteToByteArray | 494.97K | ± 7.55K | ops/s |
| openMetricsWriteToNull | 492.48K | ± 8.51K | ops/s |
| openMetricsWriteToByteArray | 485.47K | ± 5.69K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.054 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.040 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.058 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.147 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.149 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.183 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.907 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.205 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.939 | — | — |
| HistogramBenchmark.prometheusClassic | 0.665 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.674 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.645 | — | — |
| HistogramBenchmark.prometheusNative | 335793.359 | — | — |
| HistogramBenchmark.simpleclient | 0.216 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.115 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.117 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18477.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50274.637    ± 726.623  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      17537.968   ± 2574.298  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31957.540    ± 595.349  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37997.496    ± 686.141  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23143.749    ± 422.850  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21799.045    ± 387.255  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51028.195    ± 881.957  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  543269967.345 ± 17010511.297  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334019168.029 ± 616213.814  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64158.605   ± 2180.767  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  113813078.257 ± 1957196.871  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58066804.678 ± 404528.551  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55431.734   ± 1255.757  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6369.945    ± 119.813  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6534.115    ± 101.524  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6276.309     ± 90.640  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5467.754   ± 1474.006  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1035.366     ± 46.245  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4698.613    ± 730.195  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        998.624     ± 26.151  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6280.860   ± 2315.929  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11980.337    ± 191.066  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4523.078     ± 24.154  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2755.673    ± 197.800  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4389.287     ± 71.822  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30592.835   ± 1576.288  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      30199.901    ± 364.065  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485469.525   ± 5693.405  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492482.956   ± 8513.663  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494971.180   ± 7549.662  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495694.023   ± 4799.652  ops/s
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
