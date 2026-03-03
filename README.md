# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-03T05:19:51Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.54K | ± 1.46K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.23K | ± 132.34 | ops/s | 1.1x slower |
| prometheusAdd | 52.06K | ± 425.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.89K | ± 1.57K | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 26.30 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.58K | ± 179.79 | ops/s | 10.0x slower |
| simpleclientAdd | 6.27K | ± 229.80 | ops/s | 10x slower |
| openTelemetryAdd | 1.30K | ± 61.97 | ops/s | 50x slower |
| openTelemetryInc | 1.29K | ± 40.38 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.18K | ± 65.85 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.87K | ± 943.93 | ops/s | **fastest** |
| simpleclient | 4.60K | ± 46.44 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 351.62 | ops/s | 1.7x slower |
| openTelemetryClassic | 686.62 | ± 40.51 | ops/s | 7.1x slower |
| openTelemetryExponential | 541.81 | ± 12.24 | ops/s | 9.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.90K | ± 11.61K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.17K | ± 1.17K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.32K | ± 5.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.31K | ± 5.83K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49889.088   ± 1567.007  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.458     ± 61.975  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1287.843     ± 40.379  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1183.170     ± 65.853  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      52056.963    ± 425.311  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65541.370   ± 1458.082  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57233.527    ± 132.342  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6269.140    ± 229.801  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6763.210     ± 26.297  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6579.243    ± 179.786  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        686.624     ± 40.513  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.812     ± 12.238  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4866.387    ± 943.927  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2937.360    ± 351.618  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4597.558     ± 46.440  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485309.246   ± 5828.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485318.969   ± 5811.868  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489169.678   ± 1168.400  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489898.949  ± 11613.961  ops/s
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
