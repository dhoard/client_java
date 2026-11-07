# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-07T09:52:14Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 695.81M | ± 11889.55K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 211.63M | ± 2056.76K | ops/s |
| prometheusLabelValuesInc | 200.97M | ± 5566.31K | ops/s |
| prometheusLabelValuesIncSingleThread | 95.70M | ± 2181.20K | ops/s |
| prometheusInc | 67.36K | ± 992.58 | ops/s |
| prometheusNoLabelsInc | 64.56K | ± 2.09K | ops/s |
| codahaleIncNoLabels | 60.42K | ± 2.58K | ops/s |
| prometheusAdd | 54.20K | ± 528.44 | ops/s |
| openTelemetryBoundInc | 52.20K | ± 714.73 | ops/s |
| openTelemetryBoundAdd | 46.68K | ± 477.87 | ops/s |
| openTelemetryIncNoLabels | 34.27K | ± 746.33 | ops/s |
| openTelemetryInc | 33.93K | ± 1.90K | ops/s |
| openTelemetryAdd | 28.45K | ± 1.54K | ops/s |
| simpleclientInc | 10.56K | ± 271.79 | ops/s |
| simpleclientAdd | 10.23K | ± 467.07 | ops/s |
| simpleclientNoLabelsInc | 10.09K | ± 589.04 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.28K | ± 169.55 | ops/s |
| prometheusClassic | 10.35K | ± 198.93 | ops/s |
| simpleclient | 6.82K | ± 124.30 | ops/s |
| openTelemetryClassic | 6.17K | ± 1.81K | ops/s |
| openTelemetryBoundClassic | 5.84K | ± 1.93K | ops/s |
| prometheusClassicSingleThread | 4.51K | ± 26.82 | ops/s |
| prometheusNative | 4.49K | ± 358.92 | ops/s |
| openTelemetryBoundExponential | 1.17K | ± 84.21 | ops/s |
| openTelemetryExponential | 1.09K | ± 43.05 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 36.05K | ± 594.65 | ops/s |
| prometheusWriteToNull | 35.22K | ± 859.83 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 813.89K | ± 55.04K | ops/s |
| prometheusWriteToByteArray | 804.56K | ± 40.77K | ops/s |
| openMetricsWriteToByteArray | 783.46K | ± 11.27K | ops/s |
| openMetricsWriteToNull | 720.59K | ± 53.40K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.033 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.028 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.028 | — | — |
| CounterBenchmark.prometheusAdd | 0.068 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.055 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.057 | — | — |
| CounterBenchmark.simpleclientAdd | 0.093 | — | — |
| CounterBenchmark.simpleclientInc | 0.089 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.094 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.176 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.817 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.164 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.868 | — | — |
| HistogramBenchmark.prometheusClassic | 0.358 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.529 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.611 | — | — |
| HistogramBenchmark.prometheusNative | 417712.842 | — | — |
| HistogramBenchmark.simpleclient | 0.139 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.098 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.100 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      60419.915   ± 2581.279  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      28453.049   ± 1539.176  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      46681.135    ± 477.870  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      52199.959    ± 714.727  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      33933.797   ± 1902.679  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      34265.876    ± 746.334  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      54203.380    ± 528.436  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  695811505.343 ± 11889554.691  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  211625574.334 ± 2056760.907  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67355.365    ± 992.579  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  200970270.077 ± 5566310.631  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   95700090.262 ± 2181201.307  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64562.220   ± 2093.523  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10230.570    ± 467.066  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10555.131    ± 271.793  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10090.307    ± 589.038  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5838.948   ± 1930.582  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1166.262     ± 84.210  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6165.702   ± 1811.869  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1090.338     ± 43.048  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10349.570    ± 198.932  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15283.462    ± 169.553  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4510.416     ± 26.820  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4486.042    ± 358.921  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6818.117    ± 124.299  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      36052.924    ± 594.651  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35223.433    ± 859.834  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     783456.896  ± 11272.205  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     720592.446  ± 53397.606  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     804561.772  ± 40769.427  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     813889.532  ± 55043.779  ops/s
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
