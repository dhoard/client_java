# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-24T05:23:41Z
- **Commit:** [`122b09c`](https://github.com/dhoard/client_java/commit/122b09cf3af6137354c2925f9054e49271047484)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.88K | ± 1.92K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.63K | ± 1.08K | ops/s | 1.2x slower |
| prometheusAdd | 51.10K | ± 532.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.25K | ± 865.41 | ops/s | 1.4x slower |
| simpleclientInc | 6.68K | ± 116.46 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.36K | ± 74.55 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 175.75 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 213.69 | ops/s | 46x slower |
| openTelemetryInc | 1.36K | ± 178.07 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 133.78 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.55K | ± 1.53K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 155.91 | ops/s | 1.3x slower |
| prometheusNative | 3.16K | ± 142.88 | ops/s | 1.8x slower |
| openTelemetryClassic | 675.38 | ± 50.04 | ops/s | 8.2x slower |
| openTelemetryExponential | 517.05 | ± 24.15 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 461.45K | ± 16.80K | ops/s | **fastest** |
| openMetricsWriteToNull | 445.90K | ± 7.28K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 443.57K | ± 14.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 439.24K | ± 5.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48247.668    ± 865.412  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1437.086    ± 213.687  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1359.972    ± 178.068  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1311.527    ± 133.777  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51098.615    ± 532.777  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65877.215   ± 1921.460  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56632.496   ± 1075.683  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6330.857    ± 175.749  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6683.987    ± 116.457  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.173     ± 74.549  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        675.378     ± 50.045  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        517.046     ± 24.151  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5552.452   ± 1528.797  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3157.703    ± 142.883  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.625    ± 155.910  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     439235.942   ± 5112.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     445903.231   ± 7281.632  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     443569.155  ± 14705.351  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     461448.101  ± 16799.623  ops/s
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
