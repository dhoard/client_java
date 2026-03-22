# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-22T05:24:54Z
- **Commit:** [`ce5867b`](https://github.com/dhoard/client_java/commit/ce5867b3e25e10c68a6face275732b994a80ec98)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.50K | ± 1.30K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.57K | ± 1.41K | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 421.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.99K | ± 1.33K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.69K | ± 19.03 | ops/s | 9.8x slower |
| simpleclientInc | 6.67K | ± 206.62 | ops/s | 9.8x slower |
| simpleclientAdd | 6.35K | ± 304.26 | ops/s | 10x slower |
| openTelemetryInc | 1.24K | ± 44.37 | ops/s | 53x slower |
| openTelemetryAdd | 1.24K | ± 73.63 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.22K | ± 35.70 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 23.43 | ops/s | **fastest** |
| prometheusClassic | 4.18K | ± 334.39 | ops/s | 1.1x slower |
| prometheusNative | 2.87K | ± 232.18 | ops/s | 1.6x slower |
| openTelemetryClassic | 682.45 | ± 6.73 | ops/s | 6.7x slower |
| openTelemetryExponential | 580.31 | ± 8.48 | ops/s | 7.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.14K | ± 2.59K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.49K | ± 4.89K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.51K | ± 3.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.19K | ± 8.95K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48987.070   ± 1326.369  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1235.547     ± 73.628  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1239.217     ± 44.372  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1220.882     ± 35.698  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51321.624    ± 421.928  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65496.729   ± 1299.472  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55566.129   ± 1406.849  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6351.786    ± 304.262  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6671.493    ± 206.619  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6694.157     ± 19.028  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        682.445      ± 6.732  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.311      ± 8.478  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4182.498    ± 334.388  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2873.510    ± 232.179  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4571.051     ± 23.431  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472186.880   ± 8950.469  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487513.044   ± 3327.063  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491488.014   ± 4887.744  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495136.007   ± 2585.776  ops/s
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
