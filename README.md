# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-17T05:55:29Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.62K | ± 401.45 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.68K | ± 940.36 | ops/s | 1.2x slower |
| prometheusAdd | 47.94K | ± 202.03 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 41.25K | ± 6.50K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 131.09 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.15K | ± 195.33 | ops/s | 9.7x slower |
| simpleclientAdd | 5.77K | ± 66.96 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 124.59 | ops/s | 44x slower |
| openTelemetryAdd | 1.25K | ± 3.61 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.21K | ± 69.20 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.03K | ± 1.76K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 53.89 | ops/s | 1.4x slower |
| prometheusNative | 2.86K | ± 192.67 | ops/s | 2.1x slower |
| openTelemetryClassic | 597.88 | ± 13.43 | ops/s | 10x slower |
| openTelemetryExponential | 493.55 | ± 12.15 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 540.95K | ± 5.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.20K | ± 5.91K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.62K | ± 2.91K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.68K | ± 5.71K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      41251.470   ± 6499.235  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1254.621      ± 3.614  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1358.133    ± 124.590  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1210.887     ± 69.199  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47941.445    ± 202.029  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59615.802    ± 401.449  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51678.354    ± 940.363  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5772.969     ± 66.964  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6164.843    ± 131.090  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6145.159    ± 195.330  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        597.876     ± 13.434  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        493.551     ± 12.151  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6032.701   ± 1759.805  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2863.443    ± 192.668  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4373.943     ± 53.889  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514676.048   ± 5709.559  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520615.398   ± 2908.368  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526204.106   ± 5909.195  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     540953.158   ± 5354.713  ops/s
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
