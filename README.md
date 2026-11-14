# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-14T10:10:55Z
- **Commit:** [`3d95490`](https://github.com/dhoard/client_java/commit/3d95490f7bbccb162de448903e2b737946b8fa59)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 667.30M | ± 1777.34K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 369.75M | ± 570.09K | ops/s |
| prometheusLabelValuesInc | 136.95M | ± 3438.48K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.54M | ± 526.55K | ops/s |
| prometheusInc | 76.27K | ± 648.82 | ops/s |
| prometheusNoLabelsInc | 65.61K | ± 98.36 | ops/s |
| prometheusAdd | 61.82K | ± 550.80 | ops/s |
| codahaleIncNoLabels | 56.81K | ± 273.16 | ops/s |
| openTelemetryBoundInc | 44.43K | ± 918.58 | ops/s |
| openTelemetryBoundAdd | 38.51K | ± 742.42 | ops/s |
| openTelemetryInc | 27.47K | ± 46.52 | ops/s |
| openTelemetryIncNoLabels | 26.99K | ± 264.40 | ops/s |
| openTelemetryAdd | 24.27K | ± 459.18 | ops/s |
| simpleclientInc | 7.78K | ± 119.51 | ops/s |
| simpleclientNoLabelsInc | 7.57K | ± 27.77 | ops/s |
| simpleclientAdd | 7.37K | ± 438.13 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.14K | ± 504.89 | ops/s |
| prometheusClassic | 7.76K | ± 2.65K | ops/s |
| prometheusClassicSingleThread | 7.09K | ± 155.48 | ops/s |
| openTelemetryClassic | 6.32K | ± 863.76 | ops/s |
| openTelemetryBoundClassic | 6.07K | ± 1.68K | ops/s |
| simpleclient | 5.52K | ± 113.01 | ops/s |
| prometheusNative | 3.53K | ± 293.77 | ops/s |
| openTelemetryBoundExponential | 953.33 | ± 47.91 | ops/s |
| openTelemetryExponential | 867.75 | ± 30.96 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.86K | ± 355.13 | ops/s |
| openMetricsWriteToNull | 40.25K | ± 382.63 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 799.84K | ± 10.86K | ops/s |
| prometheusWriteToByteArray | 744.43K | ± 14.54K | ops/s |
| openMetricsWriteToNull | 742.33K | ± 17.71K | ops/s |
| openMetricsWriteToByteArray | 721.91K | ± 7.34K | ops/s |

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
| CounterBenchmark.prometheusAdd | 0.060 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.128 | — | — |
| CounterBenchmark.simpleclientInc | 0.121 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.125 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.165 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.991 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.151 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.085 | — | — |
| HistogramBenchmark.prometheusClassic | 0.528 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.475 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.413 | — | — |
| HistogramBenchmark.prometheusNative | 417713.054 | — | — |
| HistogramBenchmark.simpleclient | 0.173 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.088 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.086 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18466.668 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56807.790    ± 273.158  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24271.624    ± 459.179  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38508.568    ± 742.420  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      44434.371    ± 918.581  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27470.910     ± 46.521  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      26989.230    ± 264.396  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61818.617    ± 550.803  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  667304353.549 ± 1777337.624  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  369749552.567 ± 570091.289  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76272.517    ± 648.825  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  136951881.714 ± 3438481.378  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68536092.086 ± 526550.954  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65612.441     ± 98.357  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7369.293    ± 438.133  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7779.170    ± 119.513  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7570.092     ± 27.769  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6066.116   ± 1678.730  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        953.334     ± 47.911  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6320.088    ± 863.756  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        867.754     ± 30.963  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7759.545   ± 2653.891  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17143.104    ± 504.885  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7085.596    ± 155.476  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3534.837    ± 293.771  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5519.369    ± 113.011  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40248.467    ± 382.632  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40855.736    ± 355.134  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     721911.996   ± 7340.595  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     742328.854  ± 17711.383  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     744434.832  ± 14541.438  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     799838.719  ± 10856.398  ops/s
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
