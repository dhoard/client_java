# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-11T05:15:16Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.76K | ± 317.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 480.73 | ops/s | 1.2x slower |
| prometheusAdd | 51.65K | ± 188.34 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.91K | ± 1.20K | ops/s | 1.4x slower |
| simpleclientInc | 6.46K | ± 77.76 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 192.60 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 48.03 | ops/s | 11x slower |
| openTelemetryAdd | 1.42K | ± 210.58 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.34K | ± 174.62 | ops/s | 50x slower |
| openTelemetryInc | 1.26K | ± 23.04 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.32K | ± 2.07K | ops/s | **fastest** |
| simpleclient | 4.58K | ± 13.10 | ops/s | 1.4x slower |
| prometheusNative | 3.22K | ± 93.07 | ops/s | 2.0x slower |
| openTelemetryClassic | 694.39 | ± 14.26 | ops/s | 9.1x slower |
| openTelemetryExponential | 557.38 | ± 26.62 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.21K | ± 2.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.48K | ± 2.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.81K | ± 2.14K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.32K | ± 3.45K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46910.225   ± 1204.510  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1417.622    ± 210.577  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1256.069     ± 23.044  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1339.756    ± 174.617  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51646.695    ± 188.343  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66762.698    ± 317.559  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56995.977    ± 480.732  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6212.240     ± 48.029  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6463.198     ± 77.757  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6425.794    ± 192.596  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.388     ± 14.255  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.376     ± 26.624  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6315.340   ± 2074.883  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3224.975     ± 93.068  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4579.331     ± 13.097  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484321.863   ± 3451.621  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486808.270   ± 2142.465  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494481.540   ± 2411.851  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498213.297   ± 2096.781  ops/s
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
