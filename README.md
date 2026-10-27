# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-27T08:53:53Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 553.82M | ± 11671.71K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.50M | ± 542.22K | ops/s |
| prometheusLabelValuesInc | 116.17M | ± 3016.44K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.28M | ± 270.64K | ops/s |
| prometheusInc | 64.25K | ± 1.37K | ops/s |
| prometheusNoLabelsInc | 56.08K | ± 1.10K | ops/s |
| prometheusAdd | 50.99K | ± 972.55 | ops/s |
| codahaleIncNoLabels | 47.98K | ± 981.11 | ops/s |
| openTelemetryBoundInc | 37.94K | ± 478.89 | ops/s |
| openTelemetryBoundAdd | 31.73K | ± 710.62 | ops/s |
| openTelemetryInc | 22.46K | ± 943.18 | ops/s |
| openTelemetryIncNoLabels | 21.76K | ± 353.20 | ops/s |
| openTelemetryAdd | 19.38K | ± 333.88 | ops/s |
| simpleclientInc | 6.56K | ± 121.97 | ops/s |
| simpleclientNoLabelsInc | 6.38K | ± 128.29 | ops/s |
| simpleclientAdd | 6.09K | ± 284.50 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.01K | ± 158.78 | ops/s |
| prometheusClassic | 5.80K | ± 1.59K | ops/s |
| openTelemetryClassic | 5.29K | ± 1.13K | ops/s |
| openTelemetryBoundClassic | 4.59K | ± 2.11K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 30.70 | ops/s |
| simpleclient | 4.42K | ± 97.10 | ops/s |
| prometheusNative | 2.63K | ± 306.73 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 109.53 | ops/s |
| openTelemetryExponential | 1.03K | ± 43.21 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 31.23K | ± 267.13 | ops/s |
| prometheusWriteToNull | 30.65K | ± 1.44K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 497.95K | ± 6.07K | ops/s |
| prometheusWriteToByteArray | 488.61K | ± 3.10K | ops/s |
| openMetricsWriteToNull | 485.61K | ± 6.46K | ops/s |
| openMetricsWriteToByteArray | 483.10K | ± 8.09K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.020 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.048 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.042 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.154 | — | — |
| CounterBenchmark.simpleclientInc | 0.143 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.237 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.895 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.184 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.919 | — | — |
| HistogramBenchmark.prometheusClassic | 0.689 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.675 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.643 | — | — |
| HistogramBenchmark.prometheusNative | 335793.422 | — | — |
| HistogramBenchmark.simpleclient | 0.214 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.113 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.115 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.668 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47980.103    ± 981.110  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19384.271    ± 333.879  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31731.750    ± 710.624  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37944.263    ± 478.895  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22457.994    ± 943.175  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21758.632    ± 353.197  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50985.484    ± 972.548  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  553821424.278 ± 11671714.291  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334497860.306 ± 542217.659  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64254.824   ± 1365.535  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116173560.024 ± 3016440.244  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58276599.743 ± 270638.179  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56076.784   ± 1097.518  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6087.819    ± 284.498  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6561.545    ± 121.969  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6382.906    ± 128.291  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4587.054   ± 2108.866  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1052.099    ± 109.534  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5285.888   ± 1126.882  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1025.959     ± 43.210  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5798.070   ± 1589.625  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12006.979    ± 158.783  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4539.918     ± 30.702  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2630.583    ± 306.729  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.356     ± 97.104  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      31227.806    ± 267.131  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      30645.397   ± 1435.560  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483100.561   ± 8089.790  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485613.344   ± 6463.239  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488605.539   ± 3101.816  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497951.936   ± 6066.848  ops/s
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
