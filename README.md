# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-19T07:14:56Z
- **Commit:** [`0bc0408`](https://github.com/dhoard/client_java/commit/0bc040814f37610ca3bb7b1f1474dbecdb20668d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.37K | ± 1.64K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.84K | ± 707.93 | ops/s | 1.2x slower |
| prometheusAdd | 51.43K | ± 354.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.84K | ± 460.29 | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 30.70 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.34K | ± 51.87 | ops/s | 10x slower |
| simpleclientAdd | 6.11K | ± 11.92 | ops/s | 11x slower |
| openTelemetryAdd | 3.44K | ± 364.82 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.32K | ± 390.92 | ops/s | 19x slower |
| openTelemetryInc | 3.14K | ± 195.84 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.37K | ± 901.42 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 44.85 | ops/s | 1.5x slower |
| prometheusNative | 3.01K | ± 296.43 | ops/s | 2.1x slower |
| openTelemetryClassic | 750.64 | ± 34.40 | ops/s | 8.5x slower |
| openTelemetryExponential | 617.96 | ± 67.08 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.74K | ± 281.02 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.63K | ± 315.00 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.46K | ± 5.44K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.89K | ± 4.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.50K | ± 1.69K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.88K | ± 4.08K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49837.535    ± 460.285  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3435.587    ± 364.824  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3141.055    ± 195.836  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3319.439    ± 390.916  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51431.958    ± 354.809  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64371.653   ± 1635.940  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55836.672    ± 707.926  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6111.620     ± 11.921  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6557.819     ± 30.697  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.493     ± 51.875  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.637     ± 34.405  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        617.965     ± 67.076  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6367.510    ± 901.423  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.897    ± 296.430  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4387.289     ± 44.850  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23634.998    ± 315.004  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23744.805    ± 281.018  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479883.906   ± 4075.811  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491501.370   ± 1694.730  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505888.564   ± 4176.344  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508455.288   ± 5441.066  ops/s
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
