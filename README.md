# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-06T05:50:17Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 56.17K | ± 871.26 | ops/s | **fastest** |
| prometheusInc | 54.06K | ± 18.11K | ops/s | 1.0x slower |
| prometheusAdd | 51.31K | ± 375.63 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 48.27K | ± 1.54K | ops/s | 1.2x slower |
| simpleclientInc | 6.55K | ± 192.39 | ops/s | 8.6x slower |
| simpleclientNoLabelsInc | 6.36K | ± 205.74 | ops/s | 8.8x slower |
| simpleclientAdd | 6.33K | ± 226.00 | ops/s | 8.9x slower |
| openTelemetryInc | 1.52K | ± 193.91 | ops/s | 37x slower |
| openTelemetryIncNoLabels | 1.48K | ± 266.99 | ops/s | 38x slower |
| openTelemetryAdd | 1.29K | ± 75.61 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 74.60 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 361.09 | ops/s | 1.8x slower |
| openTelemetryClassic | 704.93 | ± 38.49 | ops/s | 7.4x slower |
| openTelemetryExponential | 575.83 | ± 27.67 | ops/s | 9.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.69K | ± 4.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.07K | ± 1.71K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.57K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.44K | ± 6.62K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48268.941   ± 1540.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1294.745     ± 75.608  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1520.603    ± 193.908  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1476.914    ± 266.991  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51311.375    ± 375.626  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      54056.525  ± 18106.964  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56169.185    ± 871.260  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6326.110    ± 226.003  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.368    ± 192.392  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.113    ± 205.737  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.929     ± 38.492  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.834     ± 27.669  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5235.344   ± 1751.886  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2897.282    ± 361.089  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4423.889     ± 74.597  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478443.490   ± 6622.301  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484573.777   ± 3547.170  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491070.913   ± 1711.977  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495686.573   ± 4472.505  ops/s
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
