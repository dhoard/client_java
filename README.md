# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-28T05:24:13Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.30K | ± 1.52K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.92K | ± 441.13 | ops/s | 1.2x slower |
| prometheusAdd | 51.13K | ± 493.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.45K | ± 7.28K | ops/s | 1.5x slower |
| simpleclientInc | 6.55K | ± 167.26 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.40K | ± 175.05 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 314.87 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.40K | ± 179.90 | ops/s | 47x slower |
| openTelemetryAdd | 1.40K | ± 273.06 | ops/s | 47x slower |
| openTelemetryInc | 1.23K | ± 50.07 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.83K | ± 2.78K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 36.59 | ops/s | 1.3x slower |
| prometheusNative | 3.18K | ± 85.51 | ops/s | 1.8x slower |
| openTelemetryClassic | 701.29 | ± 29.97 | ops/s | 8.3x slower |
| openTelemetryExponential | 547.79 | ± 25.53 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.20K | ± 1.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.90K | ± 2.68K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.97K | ± 2.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.35K | ± 5.12K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43454.936   ± 7283.021  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1398.511    ± 273.063  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1225.936     ± 50.071  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1401.994    ± 179.895  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51125.399    ± 493.940  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66301.777   ± 1516.731  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56922.258    ± 441.132  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6232.273    ± 314.867  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6551.737    ± 167.261  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6395.271    ± 175.045  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.290     ± 29.967  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        547.786     ± 25.525  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5829.187   ± 2784.303  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3180.882     ± 85.506  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4456.316     ± 36.587  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483966.351   ± 2896.120  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482352.244   ± 5122.674  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489899.577   ± 2681.205  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492200.748   ± 1694.848  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
