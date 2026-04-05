# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-05T05:43:20Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.83K | ± 3.41K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.21K | ± 870.46 | ops/s | 1.2x slower |
| prometheusAdd | 50.41K | ± 1.42K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.89K | ± 1.34K | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 67.17 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.60K | ± 14.83 | ops/s | 9.8x slower |
| simpleclientAdd | 6.26K | ± 359.24 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 216.91 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.33K | ± 151.48 | ops/s | 49x slower |
| openTelemetryAdd | 1.25K | ± 20.46 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.83K | ± 901.50 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 76.20 | ops/s | 1.1x slower |
| prometheusNative | 2.81K | ± 241.37 | ops/s | 1.7x slower |
| openTelemetryClassic | 679.21 | ± 21.09 | ops/s | 7.1x slower |
| openTelemetryExponential | 569.73 | ± 26.27 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.24K | ± 4.57K | ops/s | **fastest** |
| openMetricsWriteToNull | 482.50K | ± 3.02K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 479.56K | ± 5.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.89K | ± 2.58K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48890.664   ± 1341.488  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1254.630     ± 20.457  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1384.736    ± 216.912  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.735    ± 151.480  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50409.808   ± 1423.992  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64830.077   ± 3406.339  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56208.955    ± 870.461  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6261.535    ± 359.241  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6637.094     ± 67.170  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6604.717     ± 14.835  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        679.206     ± 21.090  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.735     ± 26.269  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4826.479    ± 901.499  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2809.298    ± 241.375  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4353.160     ± 76.199  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472894.995   ± 2579.641  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482499.009   ± 3017.306  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479558.340   ± 5846.858  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488235.760   ± 4568.129  ops/s
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
