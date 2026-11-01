# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-01T10:15:10Z
- **Commit:** [`e574d32`](https://github.com/dhoard/client_java/commit/e574d3226951fbecda109554024dc1f99eb8d5d5)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 278.44M | ± 11007.30K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 93.24M | ± 55.03K | ops/s |
| prometheusLabelValuesInc | 92.04M | ± 1567.97K | ops/s |
| prometheusLabelValuesIncSingleThread | 56.97M | ± 1832.82K | ops/s |
| prometheusInc | 31.40K | ± 71.84 | ops/s |
| prometheusNoLabelsInc | 30.55K | ± 1.06K | ops/s |
| openTelemetryBoundInc | 29.14K | ± 160.05 | ops/s |
| codahaleIncNoLabels | 28.99K | ± 128.16 | ops/s |
| prometheusAdd | 28.33K | ± 185.24 | ops/s |
| openTelemetryBoundAdd | 25.84K | ± 1.76K | ops/s |
| openTelemetryIncNoLabels | 21.20K | ± 2.44K | ops/s |
| openTelemetryInc | 20.40K | ± 1.35K | ops/s |
| openTelemetryAdd | 17.73K | ± 911.95 | ops/s |
| simpleclientInc | 6.40K | ± 156.15 | ops/s |
| simpleclientNoLabelsInc | 6.27K | ± 191.31 | ops/s |
| simpleclientAdd | 6.21K | ± 33.37 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.60K | ± 143.40 | ops/s |
| simpleclient | 4.07K | ± 148.50 | ops/s |
| prometheusClassic | 3.46K | ± 301.36 | ops/s |
| prometheusClassicSingleThread | 3.23K | ± 80.84 | ops/s |
| openTelemetryBoundClassic | 3.15K | ± 1.26K | ops/s |
| openTelemetryClassic | 2.91K | ± 356.66 | ops/s |
| prometheusNative | 2.03K | ± 115.16 | ops/s |
| openTelemetryBoundExponential | 628.65 | ± 47.67 | ops/s |
| openTelemetryExponential | 512.04 | ± 37.91 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 19.80K | ± 58.89 | ops/s |
| prometheusWriteToNull | 19.65K | ± 151.99 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 339.69K | ± 3.00K | ops/s |
| prometheusWriteToByteArray | 330.09K | ± 1.50K | ops/s |
| openMetricsWriteToNull | 315.74K | ± 3.45K | ops/s |
| openMetricsWriteToByteArray | 311.27K | ± 2.30K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.032 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.053 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.036 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryInc | 0.046 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.045 | — | — |
| CounterBenchmark.prometheusAdd | 0.131 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.117 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.121 | — | — |
| CounterBenchmark.simpleclientAdd | 0.151 | — | — |
| CounterBenchmark.simpleclientInc | 0.147 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.150 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.320 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.492 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.332 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.837 | — | — |
| HistogramBenchmark.prometheusClassic | 1.072 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 1.067 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.851 | — | — |
| HistogramBenchmark.prometheusNative | 335793.853 | — | — |
| HistogramBenchmark.simpleclient | 0.233 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.178 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.179 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18466.669 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28985.185    ± 128.158  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      17728.258    ± 911.950  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      25843.964   ± 1763.537  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      29135.543    ± 160.050  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      20401.009   ± 1353.288  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21200.808   ± 2439.629  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28332.750    ± 185.236  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  278436582.526 ± 11007299.788  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15   93236776.277  ± 55034.959  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31398.243     ± 71.844  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15   92040221.705 ± 1567968.441  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   56968257.254 ± 1832821.898  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30549.482   ± 1061.091  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6209.702     ± 33.367  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6399.933    ± 156.152  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6265.904    ± 191.309  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       3148.721   ± 1264.865  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        628.647     ± 47.673  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       2912.113    ± 356.665  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.043     ± 37.908  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3464.759    ± 301.363  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7598.256    ± 143.396  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3229.668     ± 80.844  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2034.121    ± 115.161  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4066.931    ± 148.495  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      19801.531     ± 58.893  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19646.258    ± 151.991  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     311267.044   ± 2301.068  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     315740.686   ± 3449.665  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     330092.995   ± 1499.551  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     339686.258   ± 3004.720  ops/s
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
