# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-22T05:52:39Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.44K | ± 421.93 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.20K | ± 2.69K | ops/s | 1.2x slower |
| prometheusAdd | 48.45K | ± 1.33K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 41.78K | ± 3.49K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.29K | ± 28.33 | ops/s | 9.5x slower |
| simpleclientInc | 6.27K | ± 56.00 | ops/s | 9.5x slower |
| simpleclientAdd | 6.00K | ± 311.55 | ops/s | 9.9x slower |
| openTelemetryInc | 1.41K | ± 134.61 | ops/s | 42x slower |
| openTelemetryAdd | 1.34K | ± 52.93 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.30K | ± 29.65 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.74K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.53K | ± 45.81 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 249.04 | ops/s | 1.9x slower |
| openTelemetryClassic | 643.35 | ± 40.29 | ops/s | 8.9x slower |
| openTelemetryExponential | 539.17 | ± 20.69 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 541.03K | ± 3.80K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 509.88K | ± 6.14K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 509.01K | ± 12.58K | ops/s | 1.1x slower |
| prometheusWriteToByteArray | 499.05K | ± 13.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41782.752   ± 3492.766  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1343.887     ± 52.926  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1405.033    ± 134.610  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1304.869     ± 29.647  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48445.806   ± 1326.832  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59441.713    ± 421.925  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50201.857   ± 2694.483  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6000.992    ± 311.546  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6267.389     ± 56.000  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6285.257     ± 28.332  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        643.349     ± 40.293  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.172     ± 20.691  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5741.402   ± 1416.609  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2998.009    ± 249.038  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4529.813     ± 45.805  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509880.580   ± 6139.085  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509006.103  ± 12579.029  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499046.599  ± 13614.448  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     541025.339   ± 3798.716  ops/s
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
