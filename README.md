# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-17T05:22:43Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.39K | ± 4.69K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.48K | ± 937.40 | ops/s | 1.1x slower |
| prometheusAdd | 48.32K | ± 139.52 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.36K | ± 1.01K | ops/s | 1.3x slower |
| simpleclientInc | 6.17K | ± 482.94 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.02K | ± 295.23 | ops/s | 9.7x slower |
| simpleclientAdd | 6.01K | ± 216.77 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.34K | ± 86.21 | ops/s | 44x slower |
| openTelemetryInc | 1.24K | ± 44.84 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.21K | ± 81.90 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.49K | ± 2.55K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 182.44 | ops/s | 1.5x slower |
| prometheusNative | 2.93K | ± 232.56 | ops/s | 2.2x slower |
| openTelemetryClassic | 580.87 | ± 2.37 | ops/s | 11x slower |
| openTelemetryExponential | 497.56 | ± 23.57 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.02K | ± 7.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 541.76K | ± 2.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.71K | ± 6.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 523.64K | ± 8.71K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43356.913   ± 1014.970  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1340.997     ± 86.205  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1244.051     ± 44.836  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1212.505     ± 81.895  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48320.816    ± 139.524  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58387.172   ± 4692.775  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51480.494    ± 937.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6007.378    ± 216.773  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6167.381    ± 482.944  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6021.294    ± 295.225  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        580.871      ± 2.372  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        497.558     ± 23.569  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6489.885   ± 2545.463  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2926.162    ± 232.559  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4452.581    ± 182.442  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     523638.750   ± 8712.817  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534706.382   ± 6339.903  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541760.316   ± 2918.188  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556019.779   ± 7298.867  ops/s
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
