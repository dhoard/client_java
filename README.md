# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-20T08:45:11Z
- **Commit:** [`d418a89`](https://github.com/dhoard/client_java/commit/d418a89b075944fe5da2c7dd8aeb72d9297ffd02)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 521.28M | ± 9079.92K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 287.29M | ± 411.86K | ops/s |
| prometheusLabelValuesInc | 108.46M | ± 2003.73K | ops/s |
| prometheusLabelValuesIncSingleThread | 52.89M | ± 333.98K | ops/s |
| prometheusInc | 59.85K | ± 172.70 | ops/s |
| prometheusNoLabelsInc | 51.07K | ± 323.67 | ops/s |
| prometheusAdd | 47.72K | ± 416.14 | ops/s |
| codahaleIncNoLabels | 43.46K | ± 2.33K | ops/s |
| openTelemetryBoundInc | 34.99K | ± 344.93 | ops/s |
| openTelemetryBoundAdd | 29.81K | ± 60.67 | ops/s |
| openTelemetryInc | 21.28K | ± 43.53 | ops/s |
| openTelemetryIncNoLabels | 20.51K | ± 545.67 | ops/s |
| openTelemetryAdd | 19.10K | ± 327.95 | ops/s |
| simpleclientInc | 6.02K | ± 109.37 | ops/s |
| simpleclientAdd | 5.93K | ± 87.76 | ops/s |
| simpleclientNoLabelsInc | 5.88K | ± 33.26 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 13.33K | ± 398.63 | ops/s |
| prometheusClassic | 6.84K | ± 730.10 | ops/s |
| openTelemetryBoundClassic | 6.39K | ± 2.56K | ops/s |
| prometheusClassicSingleThread | 5.57K | ± 28.60 | ops/s |
| openTelemetryClassic | 5.35K | ± 1.29K | ops/s |
| simpleclient | 4.47K | ± 54.78 | ops/s |
| prometheusNative | 2.78K | ± 187.32 | ops/s |
| openTelemetryBoundExponential | 742.76 | ± 22.96 | ops/s |
| openTelemetryExponential | 683.66 | ± 11.26 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.01K | ± 632.28 | ops/s |
| openMetricsWriteToNull | 26.88K | ± 805.78 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 647.49K | ± 4.75K | ops/s |
| prometheusWriteToByteArray | 634.30K | ± 8.46K | ops/s |
| openMetricsWriteToNull | 592.28K | ± 4.21K | ops/s |
| openMetricsWriteToByteArray | 585.02K | ± 3.76K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.022 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.049 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.031 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.027 | — | — |
| CounterBenchmark.openTelemetryInc | 0.044 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.046 | — | — |
| CounterBenchmark.prometheusAdd | 0.077 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.062 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.072 | — | — |
| CounterBenchmark.simpleclientAdd | 0.158 | — | — |
| CounterBenchmark.simpleclientInc | 0.156 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.159 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.170 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.271 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.186 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.374 | — | — |
| HistogramBenchmark.prometheusClassic | 0.548 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.605 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.525 | — | — |
| HistogramBenchmark.prometheusNative | 417713.345 | — | — |
| HistogramBenchmark.simpleclient | 0.211 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.131 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.131 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43456.376   ± 2328.310  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19099.096    ± 327.953  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      29812.386     ± 60.665  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      34989.114    ± 344.929  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      21281.728     ± 43.530  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      20508.483    ± 545.671  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47724.562    ± 416.140  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  521278846.053 ± 9079918.954  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  287288884.009 ± 411862.401  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59853.650    ± 172.703  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  108459183.613 ± 2003726.402  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   52885713.566 ± 333982.419  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51066.613    ± 323.674  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5927.206     ± 87.760  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6024.410    ± 109.366  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5881.127     ± 33.259  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6391.587   ± 2561.670  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        742.763     ± 22.956  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5347.299   ± 1289.814  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        683.663     ± 11.260  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6836.090    ± 730.104  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13333.636    ± 398.632  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5567.301     ± 28.598  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2775.041    ± 187.320  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.182     ± 54.776  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26884.751    ± 805.780  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27007.898    ± 632.277  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     585020.618   ± 3755.101  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     592280.586   ± 4211.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     634304.639   ± 8462.997  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     647493.703   ± 4745.822  ops/s
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
