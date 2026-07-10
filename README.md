# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-10T07:08:06Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.40K | ± 847.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.33K | ± 954.74 | ops/s | 1.2x slower |
| prometheusAdd | 47.80K | ± 710.41 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.04K | ± 290.57 | ops/s | 1.4x slower |
| simpleclientInc | 6.10K | ± 146.43 | ops/s | 9.9x slower |
| simpleclientAdd | 5.93K | ± 226.72 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.88K | ± 36.52 | ops/s | 10x slower |
| openTelemetryInc | 5.39K | ± 1.23K | ops/s | 11x slower |
| openTelemetryAdd | 4.14K | ± 904.07 | ops/s | 15x slower |
| openTelemetryIncNoLabels | 3.88K | ± 214.07 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.57K | ± 2.24K | ops/s | **fastest** |
| simpleclient | 4.23K | ± 22.80 | ops/s | 1.3x slower |
| prometheusNative | 3.13K | ± 112.91 | ops/s | 1.8x slower |
| openTelemetryClassic | 738.94 | ± 41.95 | ops/s | 7.5x slower |
| openTelemetryExponential | 573.39 | ± 20.23 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.35K | ± 199.04 | ops/s | **fastest** |
| prometheusWriteToNull | 27.30K | ± 200.15 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 561.86K | ± 2.46K | ops/s | **fastest** |
| prometheusWriteToByteArray | 558.74K | ± 2.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.09K | ± 13.66K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 520.99K | ± 2.52K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44040.791    ± 290.565  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4142.314    ± 904.069  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5386.197   ± 1228.241  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3881.207    ± 214.073  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47800.427    ± 710.407  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60396.208    ± 847.516  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51326.859    ± 954.743  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5932.384    ± 226.720  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6103.858    ± 146.427  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5882.237     ± 36.522  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        738.937     ± 41.955  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.389     ± 20.230  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5572.136   ± 2235.948  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3134.306    ± 112.911  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4233.806     ± 22.799  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27353.660    ± 199.043  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27297.819    ± 200.150  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520993.020   ± 2519.084  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521092.332  ± 13656.856  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     558741.000   ± 2312.379  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     561857.981   ± 2457.765  ops/s
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
