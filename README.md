# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-08T10:08:41Z
- **Commit:** [`85d9fb0`](https://github.com/dhoard/client_java/commit/85d9fb0dca9f064c746470e91b924d253abf8d30)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 694.34M | ± 52347.63K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 223.67M | ± 533.34K | ops/s |
| prometheusLabelValuesInc | 205.68M | ± 4259.73K | ops/s |
| prometheusLabelValuesIncSingleThread | 98.34M | ± 1696.00K | ops/s |
| prometheusInc | 69.34K | ± 650.91 | ops/s |
| prometheusNoLabelsInc | 68.18K | ± 545.99 | ops/s |
| codahaleIncNoLabels | 61.86K | ± 1.38K | ops/s |
| prometheusAdd | 58.78K | ± 2.26K | ops/s |
| openTelemetryBoundInc | 54.71K | ± 412.14 | ops/s |
| openTelemetryBoundAdd | 48.61K | ± 958.57 | ops/s |
| openTelemetryIncNoLabels | 36.20K | ± 776.66 | ops/s |
| openTelemetryInc | 35.86K | ± 439.49 | ops/s |
| openTelemetryAdd | 29.92K | ± 2.01K | ops/s |
| simpleclientInc | 11.12K | ± 129.82 | ops/s |
| simpleclientNoLabelsInc | 10.93K | ± 324.23 | ops/s |
| simpleclientAdd | 10.37K | ± 134.27 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.49K | ± 176.30 | ops/s |
| prometheusClassic | 10.30K | ± 1.18K | ops/s |
| openTelemetryClassic | 9.43K | ± 436.64 | ops/s |
| simpleclient | 7.30K | ± 165.26 | ops/s |
| openTelemetryBoundClassic | 5.79K | ± 2.79K | ops/s |
| prometheusNative | 4.66K | ± 689.21 | ops/s |
| prometheusClassicSingleThread | 4.53K | ± 47.87 | ops/s |
| openTelemetryBoundExponential | 1.28K | ± 60.30 | ops/s |
| openTelemetryExponential | 1.14K | ± 24.53 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 36.78K | ± 181.29 | ops/s |
| openMetricsWriteToNull | 36.65K | ± 216.77 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 845.36K | ± 40.06K | ops/s |
| prometheusWriteToByteArray | 827.05K | ± 31.15K | ops/s |
| openMetricsWriteToByteArray | 727.95K | ± 29.10K | ops/s |
| openMetricsWriteToNull | 722.44K | ± 27.23K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.032 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.019 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.017 | — | — |
| CounterBenchmark.openTelemetryInc | 0.026 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.026 | — | — |
| CounterBenchmark.prometheusAdd | 0.063 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.053 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.054 | — | — |
| CounterBenchmark.simpleclientAdd | 0.091 | — | — |
| CounterBenchmark.simpleclientInc | 0.085 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.086 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.191 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.749 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.101 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.830 | — | — |
| HistogramBenchmark.prometheusClassic | 0.363 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.516 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.614 | — | — |
| HistogramBenchmark.prometheusNative | 417712.817 | — | — |
| HistogramBenchmark.simpleclient | 0.131 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.096 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.096 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18504.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61857.518   ± 1382.062  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      29919.472   ± 2014.339  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      48606.436    ± 958.566  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      54713.675    ± 412.138  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      35861.889    ± 439.494  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      36196.064    ± 776.657  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58775.466   ± 2263.990  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  694335104.521 ± 52347627.175  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  223667201.587 ± 533342.313  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      69341.193    ± 650.906  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  205680617.926 ± 4259729.250  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   98344035.095 ± 1696001.416  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      68178.997    ± 545.994  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10373.619    ± 134.272  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11117.585    ± 129.817  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10931.167    ± 324.235  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5792.706   ± 2787.040  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1275.068     ± 60.299  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       9427.078    ± 436.642  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15       1137.695     ± 24.530  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10296.870   ± 1178.073  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15488.355    ± 176.303  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4526.847     ± 47.867  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4662.325    ± 689.207  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7302.401    ± 165.256  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      36651.057    ± 216.768  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      36775.077    ± 181.293  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     727954.509  ± 29095.699  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     722438.631  ± 27233.104  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     827049.852  ± 31148.154  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     845358.320  ± 40060.048  ops/s
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
