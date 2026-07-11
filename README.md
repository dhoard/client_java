# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-11T06:08:45Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.37K | ± 1.36K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.66K | ± 385.13 | ops/s | 1.2x slower |
| prometheusAdd | 50.86K | ± 765.65 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.26K | ± 823.31 | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 8.67 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.36K | ± 27.35 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 330.79 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.26K | ± 194.15 | ops/s | 20x slower |
| openTelemetryAdd | 3.22K | ± 41.91 | ops/s | 20x slower |
| openTelemetryInc | 2.90K | ± 18.36 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 1.34K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 56.63 | ops/s | 1.2x slower |
| prometheusNative | 3.01K | ± 243.46 | ops/s | 1.7x slower |
| openTelemetryClassic | 750.23 | ± 10.20 | ops/s | 7.0x slower |
| openTelemetryExponential | 578.67 | ± 20.18 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.49K | ± 301.24 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.24K | ± 906.36 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.02K | ± 5.33K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.12K | ± 4.38K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.86K | ± 4.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.44K | ± 10.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48259.812    ± 823.306  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3222.443     ± 41.908  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2902.929     ± 18.359  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3264.098    ± 194.154  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50856.933    ± 765.652  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65367.249   ± 1360.517  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56655.268    ± 385.125  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6253.943    ± 330.788  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6584.225      ± 8.674  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6360.592     ± 27.353  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.234     ± 10.199  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        578.668     ± 20.182  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5243.037   ± 1342.017  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3014.840    ± 243.464  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.769     ± 56.632  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23244.219    ± 906.356  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23486.985    ± 301.242  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470444.772  ± 10406.534  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478859.386   ± 4464.997  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485118.512   ± 4378.593  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497022.014   ± 5332.533  ops/s
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
