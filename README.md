# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-16T05:45:26Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.38K | ± 366.30 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.06K | ± 146.09 | ops/s | 1.1x slower |
| prometheusAdd | 51.60K | ± 260.46 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.32K | ± 1.14K | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 45.73 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 6.69K | ± 17.66 | ops/s | 9.5x slower |
| simpleclientAdd | 6.18K | ± 318.60 | ops/s | 10x slower |
| openTelemetryAdd | 1.27K | ± 48.90 | ops/s | 50x slower |
| openTelemetryInc | 1.23K | ± 16.57 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 21.35 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.84K | ± 1.08K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 111.71 | ops/s | 1.1x slower |
| prometheusNative | 2.76K | ± 316.07 | ops/s | 1.8x slower |
| openTelemetryClassic | 717.87 | ± 26.88 | ops/s | 6.7x slower |
| openTelemetryExponential | 570.29 | ± 11.93 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.51K | ± 5.53K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 487.39K | ± 2.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.24K | ± 4.58K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 484.03K | ± 6.11K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49321.316   ± 1144.006  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1266.026     ± 48.900  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1234.143     ± 16.572  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1201.250     ± 21.354  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51603.971    ± 260.456  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63375.681    ± 366.296  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57063.736    ± 146.093  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6182.443    ± 318.603  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6751.577     ± 45.734  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6693.349     ± 17.659  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.870     ± 26.880  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        570.290     ± 11.926  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4841.140   ± 1080.019  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2757.428    ± 316.074  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4481.857    ± 111.713  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487394.960   ± 2431.691  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485241.468   ± 4580.854  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484029.045   ± 6107.029  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494514.297   ± 5532.803  ops/s
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
