# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-02T10:28:12Z
- **Commit:** [`e574d32`](https://github.com/dhoard/client_java/commit/e574d3226951fbecda109554024dc1f99eb8d5d5)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 729.65M | ± 12206.81K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 220.61M | ± 1045.44K | ops/s |
| prometheusLabelValuesInc | 207.45M | ± 2768.42K | ops/s |
| prometheusLabelValuesIncSingleThread | 97.14M | ± 2862.22K | ops/s |
| prometheusInc | 68.59K | ± 452.14 | ops/s |
| prometheusNoLabelsInc | 66.61K | ± 927.19 | ops/s |
| codahaleIncNoLabels | 62.10K | ± 279.64 | ops/s |
| prometheusAdd | 56.99K | ± 651.58 | ops/s |
| openTelemetryBoundInc | 54.32K | ± 425.46 | ops/s |
| openTelemetryBoundAdd | 48.37K | ± 375.69 | ops/s |
| openTelemetryIncNoLabels | 35.71K | ± 418.66 | ops/s |
| openTelemetryInc | 32.55K | ± 1.98K | ops/s |
| openTelemetryAdd | 28.81K | ± 2.27K | ops/s |
| simpleclientNoLabelsInc | 11.20K | ± 58.95 | ops/s |
| simpleclientInc | 11.00K | ± 226.99 | ops/s |
| simpleclientAdd | 10.47K | ± 452.97 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.24K | ± 232.17 | ops/s |
| prometheusClassic | 9.55K | ± 3.10K | ops/s |
| openTelemetryClassic | 7.94K | ± 1.64K | ops/s |
| simpleclient | 6.97K | ± 104.49 | ops/s |
| prometheusNative | 4.86K | ± 276.22 | ops/s |
| prometheusClassicSingleThread | 4.46K | ± 59.20 | ops/s |
| openTelemetryBoundClassic | 4.16K | ± 618.96 | ops/s |
| openTelemetryBoundExponential | 1.25K | ± 100.74 | ops/s |
| openTelemetryExponential | 1.08K | ± 119.39 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 34.95K | ± 1.05K | ops/s |
| prometheusWriteToNull | 34.82K | ± 315.04 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 870.89K | ± 13.54K | ops/s |
| prometheusWriteToByteArray | 805.83K | ± 74.06K | ops/s |
| openMetricsWriteToByteArray | 779.54K | ± 11.47K | ops/s |
| openMetricsWriteToNull | 777.14K | ± 42.76K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.033 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.017 | — | — |
| CounterBenchmark.openTelemetryInc | 0.029 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.026 | — | — |
| CounterBenchmark.prometheusAdd | 0.065 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.054 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.090 | — | — |
| CounterBenchmark.simpleclientInc | 0.086 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.084 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.234 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.763 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.126 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.890 | — | — |
| HistogramBenchmark.prometheusClassic | 0.430 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.518 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.621 | — | — |
| HistogramBenchmark.prometheusNative | 335792.770 | — | — |
| HistogramBenchmark.simpleclient | 0.136 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.101 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.101 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18496.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      62103.257    ± 279.637  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      28805.313   ± 2271.220  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      48371.173    ± 375.687  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      54316.147    ± 425.461  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      32550.252   ± 1980.110  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      35707.185    ± 418.660  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56986.793    ± 651.578  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  729653510.426 ± 12206812.024  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  220606413.812 ± 1045440.416  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      68585.080    ± 452.139  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  207445786.368 ± 2768417.801  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   97135752.597 ± 2862218.347  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66613.747    ± 927.186  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10468.727    ± 452.972  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10998.448    ± 226.989  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11204.226     ± 58.950  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       4159.791    ± 618.960  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1250.195    ± 100.739  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       7943.391   ± 1644.241  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1076.657    ± 119.386  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9547.274   ± 3097.689  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15242.096    ± 232.169  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4460.817     ± 59.200  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4863.813    ± 276.221  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6970.252    ± 104.488  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34947.348   ± 1050.218  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34819.464    ± 315.036  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     779542.311  ± 11467.674  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     777143.783  ± 42758.694  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     805827.850  ± 74060.261  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     870893.745  ± 13536.104  ops/s
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
