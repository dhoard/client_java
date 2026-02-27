# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-27T05:18:11Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.30K | ± 305.57 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.16K | ± 821.47 | ops/s | 1.2x slower |
| prometheusAdd | 51.04K | ± 581.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.93K | ± 1.46K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 21.64 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.45K | ± 211.37 | ops/s | 10x slower |
| simpleclientAdd | 6.20K | ± 310.83 | ops/s | 11x slower |
| openTelemetryAdd | 1.52K | ± 393.19 | ops/s | 44x slower |
| openTelemetryInc | 1.51K | ± 165.56 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.17K | ± 38.62 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.87K | ± 1.92K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 74.64 | ops/s | 1.5x slower |
| prometheusNative | 2.83K | ± 261.61 | ops/s | 2.4x slower |
| openTelemetryClassic | 698.41 | ± 22.92 | ops/s | 9.8x slower |
| openTelemetryExponential | 541.17 | ± 12.05 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.63K | ± 1.90K | ops/s | **fastest** |
| openMetricsWriteToNull | 478.48K | ± 4.32K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.72K | ± 2.12K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 464.11K | ± 21.55K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48929.264   ± 1464.342  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1519.795    ± 393.190  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1507.039    ± 165.558  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1168.836     ± 38.622  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51035.188    ± 581.497  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66298.625    ± 305.567  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56158.417    ± 821.470  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6197.117    ± 310.829  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6778.052     ± 21.642  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6445.490    ± 211.369  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.412     ± 22.922  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.166     ± 12.053  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6873.962   ± 1923.240  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2828.623    ± 261.609  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4509.925     ± 74.637  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471721.001   ± 2118.950  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478480.389   ± 4318.052  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     464107.730  ± 21550.181  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487625.262   ± 1895.081  ops/s
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
