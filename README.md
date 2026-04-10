# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-10T05:52:51Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.44K | ± 837.66 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.00K | ± 992.56 | ops/s | 1.2x slower |
| prometheusAdd | 48.09K | ± 455.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.58K | ± 909.77 | ops/s | 1.4x slower |
| simpleclientInc | 6.34K | ± 44.03 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.28K | ± 43.08 | ops/s | 9.6x slower |
| simpleclientAdd | 5.76K | ± 135.39 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 45.06 | ops/s | 44x slower |
| openTelemetryAdd | 1.30K | ± 24.12 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.19K | ± 29.51 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 1.31K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 38.78 | ops/s | 1.2x slower |
| prometheusNative | 3.05K | ± 311.43 | ops/s | 1.7x slower |
| openTelemetryClassic | 605.01 | ± 13.91 | ops/s | 8.7x slower |
| openTelemetryExponential | 536.63 | ± 23.56 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 557.49K | ± 4.38K | ops/s | **fastest** |
| prometheusWriteToByteArray | 546.22K | ± 6.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.01K | ± 4.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 528.12K | ± 4.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44579.530    ± 909.772  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.059     ± 24.116  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1369.528     ± 45.062  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1191.631     ± 29.507  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48089.879    ± 455.309  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60440.293    ± 837.660  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52000.782    ± 992.558  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5763.369    ± 135.392  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6336.518     ± 44.030  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6277.931     ± 43.081  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        605.006     ± 13.914  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        536.631     ± 23.555  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5264.168   ± 1305.450  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3045.511    ± 311.433  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4404.167     ± 38.783  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     528124.959   ± 4381.056  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533005.756   ± 4260.494  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     546223.390   ± 6863.311  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557485.601   ± 4383.386  ops/s
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
