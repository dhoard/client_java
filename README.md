# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-10T10:51:55Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 703.75M | ± 18650.07K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 202.54M | ± 1734.34K | ops/s |
| prometheusLabelValuesInc | 191.10M | ± 3140.84K | ops/s |
| prometheusLabelValuesIncSingleThread | 92.08M | ± 1041.77K | ops/s |
| prometheusInc | 63.66K | ± 646.89 | ops/s |
| prometheusNoLabelsInc | 61.40K | ± 1.04K | ops/s |
| codahaleIncNoLabels | 59.13K | ± 2.94K | ops/s |
| prometheusAdd | 54.31K | ± 1.11K | ops/s |
| openTelemetryBoundInc | 49.39K | ± 489.05 | ops/s |
| openTelemetryBoundAdd | 44.22K | ± 460.48 | ops/s |
| openTelemetryIncNoLabels | 33.59K | ± 770.53 | ops/s |
| openTelemetryInc | 32.61K | ± 346.15 | ops/s |
| openTelemetryAdd | 27.27K | ± 1.83K | ops/s |
| simpleclientInc | 10.25K | ± 169.48 | ops/s |
| simpleclientNoLabelsInc | 10.24K | ± 58.38 | ops/s |
| simpleclientAdd | 9.81K | ± 306.34 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.26K | ± 102.90 | ops/s |
| prometheusClassic | 10.67K | ± 1.39K | ops/s |
| simpleclient | 6.33K | ± 107.16 | ops/s |
| openTelemetryClassic | 6.13K | ± 2.01K | ops/s |
| openTelemetryBoundClassic | 4.59K | ± 206.84 | ops/s |
| prometheusClassicSingleThread | 4.08K | ± 61.78 | ops/s |
| prometheusNative | 4.05K | ± 733.67 | ops/s |
| openTelemetryBoundExponential | 1.07K | ± 19.43 | ops/s |
| openTelemetryExponential | 991.14 | ± 29.42 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 32.74K | ± 529.48 | ops/s |
| prometheusWriteToNull | 32.49K | ± 508.34 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 749.34K | ± 59.49K | ops/s |
| prometheusWriteToByteArray | 723.24K | ± 35.23K | ops/s |
| openMetricsWriteToNull | 696.99K | ± 58.10K | ops/s |
| openMetricsWriteToByteArray | 648.66K | ± 11.52K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.035 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.021 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.019 | — | — |
| CounterBenchmark.openTelemetryInc | 0.029 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.028 | — | — |
| CounterBenchmark.prometheusAdd | 0.068 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.058 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.060 | — | — |
| CounterBenchmark.simpleclientAdd | 0.097 | — | — |
| CounterBenchmark.simpleclientInc | 0.092 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.092 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.208 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.890 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.168 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.956 | — | — |
| HistogramBenchmark.prometheusClassic | 0.351 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.564 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.677 | — | — |
| HistogramBenchmark.prometheusNative | 335792.960 | — | — |
| HistogramBenchmark.simpleclient | 0.149 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.108 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.109 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      59125.173   ± 2944.146  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      27274.092   ± 1830.062  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      44215.783    ± 460.480  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      49389.801    ± 489.048  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      32610.051    ± 346.149  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      33592.209    ± 770.526  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      54314.729   ± 1108.671  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  703754332.275 ± 18650069.015  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  202539720.427 ± 1734337.551  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63656.565    ± 646.894  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  191097971.046 ± 3140842.707  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   92083414.395 ± 1041767.566  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      61402.762   ± 1042.223  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9810.829    ± 306.340  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10246.304    ± 169.480  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10239.484     ± 58.375  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4590.834    ± 206.845  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1074.704     ± 19.427  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6127.578   ± 2012.036  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        991.143     ± 29.424  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10670.141   ± 1392.088  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14264.105    ± 102.899  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4075.839     ± 61.776  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4045.528    ± 733.669  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6333.555    ± 107.157  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32737.753    ± 529.478  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32487.128    ± 508.344  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     648655.834  ± 11515.074  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     696990.856  ± 58100.303  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     723242.881  ± 35234.852  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     749340.646  ± 59487.245  ops/s
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
