# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-10T05:14:23Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.45K | ± 2.54K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.45K | ± 562.24 | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 670.32 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.84K | ± 8.34K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 12.23 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.44K | ± 130.55 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 182.57 | ops/s | 10x slower |
| openTelemetryAdd | 1.38K | ± 194.85 | ops/s | 47x slower |
| openTelemetryInc | 1.29K | ± 21.18 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.25K | ± 37.41 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.91K | ± 1.87K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 22.28 | ops/s | 1.5x slower |
| prometheusNative | 3.11K | ± 220.06 | ops/s | 2.2x slower |
| openTelemetryClassic | 718.81 | ± 28.94 | ops/s | 9.6x slower |
| openTelemetryExponential | 533.20 | ± 27.01 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.89K | ± 2.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.91K | ± 1.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.70K | ± 3.05K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.62K | ± 3.42K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44841.097   ± 8342.785  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1384.576    ± 194.854  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.260     ± 21.185  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1250.612     ± 37.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51121.891    ± 670.316  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64450.396   ± 2535.746  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56453.917    ± 562.240  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6322.923    ± 182.570  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6767.974     ± 12.231  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6436.519    ± 130.549  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.812     ± 28.942  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        533.203     ± 27.005  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6913.126   ± 1874.452  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3114.470    ± 220.062  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.087     ± 22.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464620.721   ± 3420.300  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479698.748   ± 3046.587  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486912.593   ± 1727.519  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487892.775   ± 2941.861  ops/s
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
