# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-16T10:40:44Z
- **Commit:** [`3d95490`](https://github.com/dhoard/client_java/commit/3d95490f7bbccb162de448903e2b737946b8fa59)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 299.24M | ± 1930.62K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 93.15M | ± 133.69K | ops/s |
| prometheusLabelValuesInc | 92.40M | ± 2829.96K | ops/s |
| prometheusLabelValuesIncSingleThread | 57.33M | ± 459.92K | ops/s |
| prometheusNoLabelsInc | 31.18K | ± 136.75 | ops/s |
| prometheusInc | 31.18K | ± 847.44 | ops/s |
| codahaleIncNoLabels | 29.40K | ± 1.52K | ops/s |
| openTelemetryBoundInc | 29.24K | ± 396.14 | ops/s |
| openTelemetryBoundAdd | 27.33K | ± 318.00 | ops/s |
| prometheusAdd | 26.93K | ± 1.33K | ops/s |
| openTelemetryIncNoLabels | 23.21K | ± 857.61 | ops/s |
| openTelemetryInc | 22.73K | ± 587.54 | ops/s |
| openTelemetryAdd | 18.67K | ± 1.47K | ops/s |
| simpleclientInc | 6.43K | ± 246.94 | ops/s |
| simpleclientAdd | 6.07K | ± 220.68 | ops/s |
| simpleclientNoLabelsInc | 5.89K | ± 88.72 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.82K | ± 32.72 | ops/s |
| simpleclient | 3.91K | ± 59.59 | ops/s |
| openTelemetryClassic | 3.42K | ± 1.29K | ops/s |
| prometheusClassicSingleThread | 3.23K | ± 79.03 | ops/s |
| prometheusClassic | 3.16K | ± 1.17K | ops/s |
| openTelemetryBoundClassic | 2.62K | ± 114.18 | ops/s |
| prometheusNative | 1.89K | ± 94.48 | ops/s |
| openTelemetryBoundExponential | 671.05 | ± 62.43 | ops/s |
| openTelemetryExponential | 551.89 | ± 15.78 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 19.71K | ± 151.41 | ops/s |
| prometheusWriteToNull | 19.65K | ± 146.93 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 329.68K | ± 3.22K | ops/s |
| prometheusWriteToByteArray | 327.98K | ± 4.46K | ops/s |
| openMetricsWriteToNull | 306.09K | ± 5.23K | ops/s |
| openMetricsWriteToByteArray | 305.63K | ± 3.67K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.032 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.050 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.034 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryInc | 0.041 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.040 | — | — |
| CounterBenchmark.prometheusAdd | 0.137 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.118 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.119 | — | — |
| CounterBenchmark.simpleclientAdd | 0.155 | — | — |
| CounterBenchmark.simpleclientInc | 0.146 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.160 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.362 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.408 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.298 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.700 | — | — |
| HistogramBenchmark.prometheusClassic | 1.275 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 1.041 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.856 | — | — |
| HistogramBenchmark.prometheusNative | 335793.996 | — | — |
| HistogramBenchmark.simpleclient | 0.242 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.179 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.180 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.002 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29404.778   ± 1517.771  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      18669.479   ± 1467.520  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      27326.258    ± 318.004  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      29238.581    ± 396.144  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22726.454    ± 587.544  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      23206.245    ± 857.609  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      26934.479   ± 1325.813  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  299240936.258 ± 1930624.719  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15   93145144.098 ± 133685.754  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31178.282    ± 847.440  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15   92397037.862 ± 2829962.098  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   57329388.787 ± 459923.572  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31179.616    ± 136.750  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6071.881    ± 220.682  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6430.605    ± 246.942  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5888.186     ± 88.718  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       2620.622    ± 114.185  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        671.052     ± 62.428  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3416.477   ± 1290.879  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.893     ± 15.777  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3159.870   ± 1171.330  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7823.868     ± 32.723  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3225.803     ± 79.031  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1889.847     ± 94.478  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       3912.628     ± 59.593  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      19714.464    ± 151.413  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19651.150    ± 146.934  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     305629.237   ± 3674.070  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     306085.024   ± 5233.802  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     327977.550   ± 4456.888  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     329679.716   ± 3220.289  ops/s
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
