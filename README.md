# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-13T05:17:36Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 360.19 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.99K | ± 244.82 | ops/s | 1.2x slower |
| prometheusAdd | 51.67K | ± 131.09 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.04K | ± 2.18K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 24.34 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.54K | ± 183.87 | ops/s | 10x slower |
| simpleclientAdd | 6.35K | ± 220.72 | ops/s | 10x slower |
| openTelemetryAdd | 1.47K | ± 200.99 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.40K | ± 103.90 | ops/s | 48x slower |
| openTelemetryInc | 1.28K | ± 40.61 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.98K | ± 1.74K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 96.39 | ops/s | 1.6x slower |
| prometheusNative | 2.82K | ± 267.24 | ops/s | 2.5x slower |
| openTelemetryClassic | 696.64 | ± 58.91 | ops/s | 10x slower |
| openTelemetryExponential | 557.18 | ± 30.39 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 486.30K | ± 2.25K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.54K | ± 7.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.85K | ± 2.40K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.47K | ± 4.45K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49035.945   ± 2182.803  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1468.110    ± 200.991  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.910     ± 40.612  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1395.183    ± 103.901  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51670.425    ± 131.093  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66401.997    ± 360.188  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56989.603    ± 244.817  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6353.935    ± 220.718  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6776.896     ± 24.340  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6535.351    ± 183.868  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        696.640     ± 58.913  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.180     ± 30.391  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6980.171   ± 1740.829  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2821.684    ± 267.243  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4502.941     ± 96.395  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468465.279   ± 4445.564  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473846.365   ± 2402.927  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479542.786   ± 7389.664  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486295.741   ± 2252.396  ops/s
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
