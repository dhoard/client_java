# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-09T05:21:30Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.62K | ± 548.75 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.70K | ± 877.91 | ops/s | 1.2x slower |
| prometheusAdd | 49.24K | ± 622.27 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.20K | ± 521.32 | ops/s | 1.3x slower |
| simpleclientInc | 6.44K | ± 32.89 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.02K | ± 303.98 | ops/s | 9.9x slower |
| simpleclientAdd | 5.99K | ± 226.41 | ops/s | 9.9x slower |
| openTelemetryAdd | 1.39K | ± 92.37 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.35K | ± 28.93 | ops/s | 44x slower |
| openTelemetryInc | 1.35K | ± 50.75 | ops/s | 44x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.98K | ± 1.19K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 66.62 | ops/s | 1.4x slower |
| prometheusNative | 3.01K | ± 252.44 | ops/s | 2.0x slower |
| openTelemetryClassic | 634.41 | ± 16.12 | ops/s | 9.4x slower |
| openTelemetryExponential | 527.77 | ± 14.14 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 532.77K | ± 8.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.64K | ± 2.64K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 515.35K | ± 8.30K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 503.77K | ± 4.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44198.447    ± 521.324  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1386.318     ± 92.369  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1348.791     ± 50.749  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1351.567     ± 28.928  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49238.097    ± 622.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59619.843    ± 548.754  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51702.843    ± 877.912  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5994.589    ± 226.406  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6437.100     ± 32.890  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6019.896    ± 303.985  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        634.413     ± 16.124  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        527.766     ± 14.137  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5975.095   ± 1187.197  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3013.887    ± 252.441  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4372.693     ± 66.615  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     503772.823   ± 4407.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     515348.400   ± 8299.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525636.755   ± 2637.496  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     532769.133   ± 8513.951  ops/s
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
