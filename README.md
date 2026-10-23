# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-23T08:37:04Z
- **Commit:** [`ec63f9b`](https://github.com/dhoard/client_java/commit/ec63f9be83f5f079424be2a29f319f7175f54c9e)
- **JDK:** 25.0.4.1 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1017-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 680.29M | ± 1523.30K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.51M | ± 400.11K | ops/s |
| prometheusLabelValuesInc | 141.24M | ± 2276.73K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.82M | ± 680.49K | ops/s |
| prometheusInc | 76.89K | ± 590.78 | ops/s |
| prometheusNoLabelsInc | 67.60K | ± 708.26 | ops/s |
| prometheusAdd | 62.29K | ± 216.49 | ops/s |
| codahaleIncNoLabels | 55.89K | ± 1.86K | ops/s |
| openTelemetryBoundInc | 44.66K | ± 165.98 | ops/s |
| openTelemetryBoundAdd | 38.83K | ± 598.01 | ops/s |
| openTelemetryIncNoLabels | 27.78K | ± 784.41 | ops/s |
| openTelemetryInc | 27.51K | ± 84.97 | ops/s |
| openTelemetryAdd | 24.10K | ± 773.06 | ops/s |
| simpleclientInc | 7.77K | ± 49.03 | ops/s |
| simpleclientNoLabelsInc | 7.60K | ± 14.37 | ops/s |
| simpleclientAdd | 7.57K | ± 131.35 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.45K | ± 121.27 | ops/s |
| prometheusClassic | 10.80K | ± 1.80K | ops/s |
| openTelemetryBoundClassic | 7.87K | ± 2.79K | ops/s |
| prometheusClassicSingleThread | 7.10K | ± 59.75 | ops/s |
| openTelemetryClassic | 5.82K | ± 1.49K | ops/s |
| simpleclient | 5.79K | ± 115.97 | ops/s |
| prometheusNative | 3.39K | ± 274.56 | ops/s |
| openTelemetryBoundExponential | 971.55 | ± 64.75 | ops/s |
| openTelemetryExponential | 886.75 | ± 22.70 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 40.64K | ± 276.23 | ops/s |
| openMetricsWriteToNull | 40.53K | ± 256.41 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 756.42K | ± 3.55K | ops/s |
| prometheusWriteToByteArray | 747.59K | ± 5.67K | ops/s |
| openMetricsWriteToNull | 718.64K | ± 9.54K | ops/s |
| openMetricsWriteToByteArray | 705.85K | ± 8.96K | ops/s |

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
| CounterBenchmark.openTelemetryIncNoLabels | 0.034 | — | — |
| CounterBenchmark.prometheusAdd | 0.059 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.055 | — | — |
| CounterBenchmark.simpleclientAdd | 0.125 | — | — |
| CounterBenchmark.simpleclientInc | 0.122 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.125 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.132 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.977 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.173 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.062 | — | — |
| HistogramBenchmark.prometheusClassic | 0.351 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.464 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.411 | — | — |
| HistogramBenchmark.prometheusNative | 417713.112 | — | — |
| HistogramBenchmark.simpleclient | 0.162 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.087 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18504.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55891.417   ± 1863.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24101.371    ± 773.059  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      38827.380    ± 598.011  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      44658.650    ± 165.975  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27513.785     ± 84.966  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      27783.334    ± 784.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62289.644    ± 216.492  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  680291369.812 ± 1523295.846  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370510191.200 ± 400112.933  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76887.999    ± 590.779  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  141235589.289 ± 2276727.224  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68816560.600 ± 680492.271  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67595.823    ± 708.259  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7565.527    ± 131.345  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7772.077     ± 49.030  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7603.805     ± 14.367  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       7868.723   ± 2792.100  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        971.548     ± 64.754  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5820.143   ± 1487.589  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        886.750     ± 22.701  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10798.853   ± 1800.585  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17453.760    ± 121.273  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7103.258     ± 59.752  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3387.592    ± 274.565  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5793.104    ± 115.969  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40534.413    ± 256.414  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40644.583    ± 276.234  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     705854.199   ± 8961.960  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     718636.450   ± 9544.401  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     747587.262   ± 5671.923  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     756423.490   ± 3545.866  ops/s
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
