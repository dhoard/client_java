# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-30T09:47:07Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 704.48M | ± 23197.38K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 211.52M | ± 3422.46K | ops/s |
| prometheusLabelValuesInc | 193.16M | ± 8582.90K | ops/s |
| prometheusLabelValuesIncSingleThread | 91.23M | ± 1089.60K | ops/s |
| prometheusInc | 65.46K | ± 485.82 | ops/s |
| prometheusNoLabelsInc | 62.44K | ± 968.90 | ops/s |
| codahaleIncNoLabels | 61.18K | ± 935.02 | ops/s |
| prometheusAdd | 56.44K | ± 2.40K | ops/s |
| openTelemetryBoundInc | 53.35K | ± 946.77 | ops/s |
| openTelemetryBoundAdd | 47.72K | ± 731.86 | ops/s |
| openTelemetryIncNoLabels | 34.44K | ± 615.98 | ops/s |
| openTelemetryInc | 34.30K | ± 487.99 | ops/s |
| openTelemetryAdd | 28.79K | ± 2.05K | ops/s |
| simpleclientInc | 10.66K | ± 309.70 | ops/s |
| simpleclientNoLabelsInc | 10.51K | ± 253.47 | ops/s |
| simpleclientAdd | 9.91K | ± 643.31 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.07K | ± 92.62 | ops/s |
| prometheusClassic | 9.34K | ± 2.92K | ops/s |
| simpleclient | 6.83K | ± 67.50 | ops/s |
| openTelemetryClassic | 6.47K | ± 1.86K | ops/s |
| openTelemetryBoundClassic | 5.58K | ± 1.80K | ops/s |
| prometheusClassicSingleThread | 4.36K | ± 52.54 | ops/s |
| prometheusNative | 4.28K | ± 340.04 | ops/s |
| openTelemetryBoundExponential | 1.05K | ± 54.29 | ops/s |
| openTelemetryExponential | 1.02K | ± 29.11 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 34.71K | ± 779.75 | ops/s |
| prometheusWriteToNull | 34.40K | ± 695.98 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 845.42K | ± 17.02K | ops/s |
| prometheusWriteToNull | 826.95K | ± 42.93K | ops/s |
| openMetricsWriteToNull | 719.36K | ± 35.25K | ops/s |
| openMetricsWriteToByteArray | 718.64K | ± 47.04K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.033 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.028 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.027 | — | — |
| CounterBenchmark.prometheusAdd | 0.066 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.059 | — | — |
| CounterBenchmark.simpleclientAdd | 0.096 | — | — |
| CounterBenchmark.simpleclientInc | 0.089 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.090 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.182 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.901 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.158 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.925 | — | — |
| HistogramBenchmark.prometheusClassic | 0.438 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.542 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.655 | — | — |
| HistogramBenchmark.prometheusNative | 417712.886 | — | — |
| HistogramBenchmark.simpleclient | 0.139 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.102 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.102 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.667 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61182.718    ± 935.016  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      28789.641   ± 2051.262  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      47720.795    ± 731.862  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      53351.587    ± 946.772  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      34296.059    ± 487.987  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      34443.854    ± 615.978  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56438.586   ± 2396.655  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  704481260.586 ± 23197376.062  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  211522054.660 ± 3422462.856  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65457.930    ± 485.820  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  193157114.288 ± 8582899.153  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   91233532.594 ± 1089596.528  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      62442.061    ± 968.898  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9910.700    ± 643.314  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10660.024    ± 309.698  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10510.045    ± 253.466  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5581.519   ± 1802.939  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1053.484     ± 54.288  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6468.936   ± 1864.698  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1024.596     ± 29.108  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9336.747   ± 2921.659  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15066.714     ± 92.615  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4357.336     ± 52.542  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4281.146    ± 340.044  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6834.516     ± 67.496  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34705.778    ± 779.748  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34395.855    ± 695.984  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     718640.271  ± 47040.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     719355.392  ± 35251.498  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     845416.758  ± 17017.038  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     826949.858  ± 42927.587  ops/s
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
