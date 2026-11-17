# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-17T11:47:48Z
- **Commit:** [`3ea508f`](https://github.com/dhoard/client_java/commit/3ea508f61ddaa1f8b43266e3bf378d7f60e14f25)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 676.50M | ± 15796.89K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.17M | ± 424.28K | ops/s |
| prometheusLabelValuesInc | 134.99M | ± 5935.41K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.24M | ± 235.54K | ops/s |
| prometheusInc | 77.45K | ± 1.36K | ops/s |
| prometheusNoLabelsInc | 65.40K | ± 127.04 | ops/s |
| prometheusAdd | 62.46K | ± 133.18 | ops/s |
| codahaleIncNoLabels | 57.20K | ± 575.29 | ops/s |
| openTelemetryBoundInc | 45.11K | ± 463.05 | ops/s |
| openTelemetryBoundAdd | 38.99K | ± 738.44 | ops/s |
| openTelemetryInc | 27.66K | ± 179.02 | ops/s |
| openTelemetryIncNoLabels | 27.13K | ± 141.17 | ops/s |
| openTelemetryAdd | 24.03K | ± 44.68 | ops/s |
| simpleclientInc | 7.84K | ± 126.04 | ops/s |
| simpleclientNoLabelsInc | 7.62K | ± 213.44 | ops/s |
| simpleclientAdd | 7.48K | ± 240.71 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.56K | ± 35.99 | ops/s |
| prometheusClassic | 10.18K | ± 1.89K | ops/s |
| prometheusClassicSingleThread | 7.18K | ± 11.01 | ops/s |
| simpleclient | 5.85K | ± 76.60 | ops/s |
| openTelemetryClassic | 5.84K | ± 1.00K | ops/s |
| openTelemetryBoundClassic | 5.02K | ± 451.45 | ops/s |
| prometheusNative | 3.51K | ± 308.30 | ops/s |
| openTelemetryExponential | 900.78 | ± 12.55 | ops/s |
| openTelemetryBoundExponential | 891.22 | ± 20.24 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.76K | ± 350.06 | ops/s |
| openMetricsWriteToNull | 40.42K | ± 133.80 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 778.49K | ± 11.51K | ops/s |
| prometheusWriteToByteArray | 747.74K | ± 17.99K | ops/s |
| openMetricsWriteToNull | 712.41K | ± 9.39K | ops/s |
| openMetricsWriteToByteArray | 711.57K | ± 9.16K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.024 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.021 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.035 | — | — |
| CounterBenchmark.prometheusAdd | 0.059 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.057 | — | — |
| CounterBenchmark.simpleclientAdd | 0.126 | — | — |
| CounterBenchmark.simpleclientInc | 0.120 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.124 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.190 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.059 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.165 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.050 | — | — |
| HistogramBenchmark.prometheusClassic | 0.372 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.459 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.407 | — | — |
| HistogramBenchmark.prometheusNative | 417713.066 | — | — |
| HistogramBenchmark.simpleclient | 0.161 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.086 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57195.310    ± 575.288  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24030.375     ± 44.683  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38992.013    ± 738.436  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      45106.668    ± 463.051  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27657.756    ± 179.021  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      27129.400    ± 141.170  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62457.458    ± 133.182  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  676495919.764 ± 15796891.177  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370170826.788 ± 424282.898  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77447.851   ± 1359.560  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  134994941.300 ± 5935407.537  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68240955.753 ± 235538.923  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65398.078    ± 127.037  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7476.196    ± 240.714  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7836.759    ± 126.039  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7622.409    ± 213.442  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5015.080    ± 451.448  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        891.220     ± 20.241  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5841.662   ± 1000.363  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        900.784     ± 12.549  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10181.889   ± 1889.061  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17561.814     ± 35.987  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7178.202     ± 11.014  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3509.312    ± 308.299  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5853.263     ± 76.601  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40423.925    ± 133.804  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40759.098    ± 350.057  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     711568.580   ± 9159.670  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     712405.077   ± 9387.514  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     747735.615  ± 17990.321  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     778492.941  ± 11510.854  ops/s
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
