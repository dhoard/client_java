# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-01T06:48:24Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 56.88K | ± 426.25 | ops/s | **fastest** |
| prometheusInc | 55.57K | ± 17.67K | ops/s | 1.0x slower |
| prometheusAdd | 50.98K | ± 443.07 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 49.85K | ± 974.13 | ops/s | 1.1x slower |
| simpleclientInc | 6.71K | ± 8.06 | ops/s | 8.5x slower |
| simpleclientNoLabelsInc | 6.43K | ± 253.92 | ops/s | 8.8x slower |
| simpleclientAdd | 6.20K | ± 205.63 | ops/s | 9.2x slower |
| openTelemetryInc | 1.43K | ± 226.94 | ops/s | 40x slower |
| openTelemetryAdd | 1.26K | ± 53.23 | ops/s | 45x slower |
| openTelemetryIncNoLabels | 1.21K | ± 55.13 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.86K | ± 1.84K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 82.55 | ops/s | 1.3x slower |
| prometheusNative | 2.85K | ± 299.51 | ops/s | 2.1x slower |
| openTelemetryClassic | 684.10 | ± 34.22 | ops/s | 8.6x slower |
| openTelemetryExponential | 524.64 | ± 10.87 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.05K | ± 1.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.63K | ± 1.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.82K | ± 1.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.56K | ± 4.45K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49850.627    ± 974.134  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1264.081     ± 53.227  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1433.528    ± 226.944  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1213.589     ± 55.133  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50984.460    ± 443.068  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      55568.591  ± 17666.768  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56881.964    ± 426.252  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6203.664    ± 205.626  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6705.236      ± 8.056  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6433.702    ± 253.916  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.102     ± 34.220  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.639     ± 10.874  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5863.952   ± 1837.076  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2845.709    ± 299.511  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.983     ± 82.547  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482557.252   ± 4449.721  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489823.402   ± 1539.668  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492626.446   ± 1821.679  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494047.694   ± 1765.349  ops/s
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
