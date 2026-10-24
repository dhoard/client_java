# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-24T08:34:01Z
- **Commit:** [`533375f`](https://github.com/dhoard/client_java/commit/533375f65bc9130d9ea88ca139784bfb966b04f7)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 680.81M | ± 18779.90K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 210.15M | ± 2669.51K | ops/s |
| prometheusLabelValuesInc | 196.08M | ± 2541.12K | ops/s |
| prometheusLabelValuesIncSingleThread | 92.24M | ± 946.38K | ops/s |
| prometheusInc | 65.23K | ± 658.43 | ops/s |
| prometheusNoLabelsInc | 63.21K | ± 504.63 | ops/s |
| codahaleIncNoLabels | 57.81K | ± 715.36 | ops/s |
| prometheusAdd | 56.38K | ± 1.85K | ops/s |
| openTelemetryBoundInc | 52.02K | ± 402.12 | ops/s |
| openTelemetryBoundAdd | 46.56K | ± 328.22 | ops/s |
| openTelemetryIncNoLabels | 35.29K | ± 744.89 | ops/s |
| openTelemetryInc | 34.83K | ± 319.33 | ops/s |
| openTelemetryAdd | 27.21K | ± 302.99 | ops/s |
| simpleclientInc | 10.33K | ± 285.49 | ops/s |
| simpleclientNoLabelsInc | 10.29K | ± 125.91 | ops/s |
| simpleclientAdd | 9.51K | ± 110.98 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.82K | ± 108.86 | ops/s |
| prometheusClassic | 10.04K | ± 1.10K | ops/s |
| openTelemetryClassic | 8.43K | ± 74.17 | ops/s |
| openTelemetryBoundClassic | 6.96K | ± 1.87K | ops/s |
| simpleclient | 6.65K | ± 144.14 | ops/s |
| prometheusClassicSingleThread | 4.25K | ± 53.94 | ops/s |
| prometheusNative | 4.16K | ± 225.25 | ops/s |
| openTelemetryBoundExponential | 1.12K | ± 19.28 | ops/s |
| openTelemetryExponential | 1.04K | ± 53.62 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 34.41K | ± 393.00 | ops/s |
| openMetricsWriteToNull | 34.34K | ± 440.48 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 818.99K | ± 74.70K | ops/s |
| prometheusWriteToByteArray | 724.58K | ± 8.58K | ops/s |
| openMetricsWriteToNull | 718.22K | ± 23.71K | ops/s |
| openMetricsWriteToByteArray | 692.81K | ± 62.47K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.035 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.027 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.027 | — | — |
| CounterBenchmark.prometheusAdd | 0.065 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.059 | — | — |
| CounterBenchmark.simpleclientAdd | 0.099 | — | — |
| CounterBenchmark.simpleclientInc | 0.092 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.092 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.147 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.849 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.113 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.912 | — | — |
| HistogramBenchmark.prometheusClassic | 0.372 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.541 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.650 | — | — |
| HistogramBenchmark.prometheusNative | 417712.901 | — | — |
| HistogramBenchmark.simpleclient | 0.143 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.103 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.102 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57808.922    ± 715.359  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      27213.077    ± 302.994  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      46562.059    ± 328.223  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      52021.897    ± 402.118  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      34830.707    ± 319.328  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      35293.969    ± 744.894  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56384.203   ± 1851.707  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  680808208.787 ± 18779899.835  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  210151932.553 ± 2669507.595  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65233.759    ± 658.431  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  196084435.122 ± 2541124.234  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   92243234.834 ± 946380.193  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63205.686    ± 504.634  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       9505.201    ± 110.984  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10334.252    ± 285.487  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10292.946    ± 125.912  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6960.697   ± 1866.981  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1116.424     ± 19.281  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       8431.264     ± 74.167  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1038.574     ± 53.623  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10039.655   ± 1102.627  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14821.791    ± 108.858  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4249.624     ± 53.943  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4156.245    ± 225.254  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6654.172    ± 144.138  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34336.823    ± 440.483  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34413.790    ± 393.001  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     692806.789  ± 62472.426  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     718219.221  ± 23713.825  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     724584.040   ± 8577.611  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     818987.220  ± 74704.302  ops/s
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
