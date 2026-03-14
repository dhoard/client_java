# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-14T05:16:14Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.38K | ± 305.92 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.93K | ± 371.51 | ops/s | 1.2x slower |
| prometheusAdd | 51.74K | ± 97.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.37K | ± 1.48K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 127.29 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.58K | ± 189.57 | ops/s | 10x slower |
| simpleclientAdd | 6.54K | ± 13.98 | ops/s | 10x slower |
| openTelemetryAdd | 1.58K | ± 254.16 | ops/s | 42x slower |
| openTelemetryInc | 1.26K | ± 8.61 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.21K | ± 33.43 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.30K | ± 2.12K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 16.58 | ops/s | 1.4x slower |
| prometheusNative | 2.91K | ± 205.52 | ops/s | 2.2x slower |
| openTelemetryClassic | 708.85 | ± 56.48 | ops/s | 8.9x slower |
| openTelemetryExponential | 568.20 | ± 46.26 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.58K | ± 3.13K | ops/s | **fastest** |
| openMetricsWriteToNull | 484.81K | ± 3.01K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 478.16K | ± 10.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 466.38K | ± 6.11K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48365.265   ± 1483.665  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1583.816    ± 254.156  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1263.013      ± 8.605  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1214.179     ± 33.433  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51735.998     ± 97.619  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66383.979    ± 305.923  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56928.618    ± 371.507  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6539.147     ± 13.977  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6689.243    ± 127.294  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6583.865    ± 189.569  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.846     ± 56.476  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.201     ± 46.263  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6298.533   ± 2118.075  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2913.195    ± 205.524  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4557.199     ± 16.578  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     466377.301   ± 6113.182  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484808.906   ± 3007.748  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478155.589  ± 10341.877  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488581.234   ± 3125.175  ops/s
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
