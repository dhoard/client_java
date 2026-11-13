# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-13T10:49:38Z
- **Commit:** [`3d95490`](https://github.com/dhoard/client_java/commit/3d95490f7bbccb162de448903e2b737946b8fa59)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 540.06M | ± 31887.42K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.41M | ± 775.37K | ops/s |
| prometheusLabelValuesInc | 115.99M | ± 2214.81K | ops/s |
| prometheusLabelValuesIncSingleThread | 57.17M | ± 2014.61K | ops/s |
| prometheusInc | 65.18K | ± 1.54K | ops/s |
| prometheusNoLabelsInc | 56.48K | ± 1.02K | ops/s |
| prometheusAdd | 50.90K | ± 1.06K | ops/s |
| codahaleIncNoLabels | 50.11K | ± 916.03 | ops/s |
| openTelemetryBoundInc | 37.49K | ± 472.31 | ops/s |
| openTelemetryBoundAdd | 31.36K | ± 674.28 | ops/s |
| openTelemetryInc | 23.02K | ± 390.31 | ops/s |
| openTelemetryIncNoLabels | 22.38K | ± 1.42K | ops/s |
| openTelemetryAdd | 19.20K | ± 318.58 | ops/s |
| simpleclientInc | 6.57K | ± 108.10 | ops/s |
| simpleclientNoLabelsInc | 6.31K | ± 106.03 | ops/s |
| simpleclientAdd | 6.27K | ± 207.68 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.97K | ± 187.99 | ops/s |
| prometheusClassic | 5.96K | ± 843.30 | ops/s |
| openTelemetryBoundClassic | 5.09K | ± 1.88K | ops/s |
| prometheusClassicSingleThread | 4.53K | ± 18.57 | ops/s |
| simpleclient | 4.46K | ± 69.17 | ops/s |
| openTelemetryClassic | 4.07K | ± 411.04 | ops/s |
| prometheusNative | 2.76K | ± 373.76 | ops/s |
| openTelemetryBoundExponential | 993.06 | ± 84.32 | ops/s |
| openTelemetryExponential | 967.89 | ± 24.45 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 30.86K | ± 1.34K | ops/s |
| prometheusWriteToNull | 29.66K | ± 1.03K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 508.31K | ± 5.33K | ops/s |
| prometheusWriteToByteArray | 503.18K | ± 3.38K | ops/s |
| openMetricsWriteToNull | 499.61K | ± 5.17K | ops/s |
| openMetricsWriteToByteArray | 491.34K | ± 4.19K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.049 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.042 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.149 | — | — |
| CounterBenchmark.simpleclientInc | 0.142 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.148 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.200 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.951 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.233 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.970 | — | — |
| HistogramBenchmark.prometheusClassic | 0.630 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.688 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.643 | — | — |
| HistogramBenchmark.prometheusNative | 417713.366 | — | — |
| HistogramBenchmark.simpleclient | 0.210 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.114 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.119 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18496.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50106.513    ± 916.034  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      19204.033    ± 318.580  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31355.791    ± 674.276  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37487.200    ± 472.311  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      23023.380    ± 390.305  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22379.032   ± 1415.203  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50896.014   ± 1063.067  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  540063492.515 ± 31887418.212  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334407027.618 ± 775373.893  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65183.715   ± 1544.078  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  115991414.320 ± 2214810.822  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   57166297.070 ± 2014609.315  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56483.069   ± 1015.586  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6271.955    ± 207.680  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6572.987    ± 108.098  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6306.511    ± 106.029  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5091.478   ± 1884.997  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        993.059     ± 84.320  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4074.646    ± 411.038  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        967.890     ± 24.455  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5956.066    ± 843.297  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11971.574    ± 187.992  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4526.675     ± 18.575  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2760.731    ± 373.758  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.762     ± 69.171  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      30856.904   ± 1341.131  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      29659.515   ± 1030.236  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     491335.940   ± 4191.449  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     499607.804   ± 5166.839  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503176.518   ± 3376.990  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508313.811   ± 5332.759  ops/s
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
