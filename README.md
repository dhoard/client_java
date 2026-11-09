# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-09T10:45:09Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 676.37M | ± 7464.42K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.39M | ± 304.72K | ops/s |
| prometheusLabelValuesInc | 138.03M | ± 2404.52K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.53M | ± 212.50K | ops/s |
| prometheusInc | 76.54K | ± 596.96 | ops/s |
| prometheusNoLabelsInc | 67.22K | ± 627.30 | ops/s |
| prometheusAdd | 62.31K | ± 168.12 | ops/s |
| codahaleIncNoLabels | 56.55K | ± 368.39 | ops/s |
| openTelemetryBoundInc | 45.06K | ± 534.24 | ops/s |
| openTelemetryBoundAdd | 38.42K | ± 112.38 | ops/s |
| openTelemetryInc | 27.52K | ± 274.68 | ops/s |
| openTelemetryIncNoLabels | 27.15K | ± 214.62 | ops/s |
| openTelemetryAdd | 24.07K | ± 47.40 | ops/s |
| simpleclientInc | 7.81K | ± 99.08 | ops/s |
| simpleclientNoLabelsInc | 7.66K | ± 91.59 | ops/s |
| simpleclientAdd | 7.58K | ± 152.36 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.56K | ± 84.87 | ops/s |
| prometheusClassic | 7.35K | ± 2.42K | ops/s |
| prometheusClassicSingleThread | 7.20K | ± 18.98 | ops/s |
| openTelemetryBoundClassic | 6.61K | ± 1.63K | ops/s |
| openTelemetryClassic | 6.09K | ± 1.31K | ops/s |
| simpleclient | 5.85K | ± 59.59 | ops/s |
| prometheusNative | 3.55K | ± 278.62 | ops/s |
| openTelemetryBoundExponential | 997.48 | ± 67.87 | ops/s |
| openTelemetryExponential | 879.40 | ± 49.14 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.68K | ± 412.09 | ops/s |
| openMetricsWriteToNull | 40.49K | ± 192.62 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 782.66K | ± 8.87K | ops/s |
| prometheusWriteToByteArray | 755.49K | ± 13.53K | ops/s |
| openMetricsWriteToNull | 732.24K | ± 4.70K | ops/s |
| openMetricsWriteToByteArray | 718.75K | ± 22.68K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.017 | — | — |
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
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.124 | — | — |
| CounterBenchmark.simpleclientInc | 0.120 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.123 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.150 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.948 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.161 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.076 | — | — |
| HistogramBenchmark.prometheusClassic | 0.548 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.462 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.406 | — | — |
| HistogramBenchmark.prometheusNative | 417713.056 | — | — |
| HistogramBenchmark.simpleclient | 0.162 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.087 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18496.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56549.578    ± 368.394  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24067.535     ± 47.401  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38417.673    ± 112.378  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      45062.916    ± 534.243  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27521.496    ± 274.677  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      27153.019    ± 214.615  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62313.504    ± 168.123  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  676366084.176 ± 7464421.045  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370390379.768 ± 304716.192  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76538.789    ± 596.964  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  138030572.078 ± 2404517.555  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68527595.811 ± 212501.724  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67218.119    ± 627.295  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7578.448    ± 152.362  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7808.587     ± 99.085  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7662.952     ± 91.590  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6608.786   ± 1631.024  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        997.481     ± 67.871  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6088.257   ± 1312.640  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        879.399     ± 49.141  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7354.797   ± 2424.909  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17556.081     ± 84.869  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7201.508     ± 18.978  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3553.667    ± 278.616  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5845.514     ± 59.595  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40492.630    ± 192.618  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40680.327    ± 412.087  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     718745.989  ± 22677.883  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     732241.320   ± 4703.334  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     755489.099  ± 13529.708  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     782664.130   ± 8865.872  ops/s
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
