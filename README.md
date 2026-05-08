# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-08T06:04:25Z
- **Commit:** [`317347c`](https://github.com/dhoard/client_java/commit/317347c6ab5ee6f2ed5c963bb71f39b2a1d624be)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.47K | ± 1.97K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.28K | ± 173.31 | ops/s | 1.1x slower |
| prometheusAdd | 51.04K | ± 191.12 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.86K | ± 9.27K | ops/s | 1.4x slower |
| simpleclientInc | 6.51K | ± 6.52 | ops/s | 9.9x slower |
| simpleclientAdd | 6.48K | ± 65.12 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 33.91 | ops/s | 10x slower |
| openTelemetryAdd | 3.36K | ± 440.46 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.23K | ± 505.93 | ops/s | 20x slower |
| openTelemetryInc | 2.76K | ± 32.01 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.03K | ± 677.60 | ops/s | **fastest** |
| simpleclient | 4.46K | ± 74.76 | ops/s | 1.1x slower |
| prometheusNative | 3.16K | ± 98.08 | ops/s | 1.6x slower |
| openTelemetryClassic | 762.20 | ± 29.93 | ops/s | 6.6x slower |
| openTelemetryExponential | 648.14 | ± 90.61 | ops/s | 7.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.69K | ± 281.58 | ops/s | **fastest** |
| openMetricsWriteToNull | 22.96K | ± 845.02 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 509.64K | ± 8.15K | ops/s | **fastest** |
| prometheusWriteToByteArray | 498.46K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.33K | ± 4.00K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.14K | ± 2.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44861.852   ± 9267.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3362.567    ± 440.463  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2762.854     ± 32.012  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3233.452    ± 505.933  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51038.513    ± 191.121  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64469.145   ± 1967.059  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57277.885    ± 173.315  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6481.616     ± 65.123  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6511.177      ± 6.520  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6382.585     ± 33.915  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        762.204     ± 29.926  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        648.137     ± 90.610  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5028.500    ± 677.598  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3158.600     ± 98.085  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.726     ± 74.759  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22963.544    ± 845.018  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23694.436    ± 281.580  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482135.473   ± 2816.654  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487328.662   ± 4003.138  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498461.277   ± 5060.262  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509641.353   ± 8152.836  ops/s
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
