# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-21T05:12:18Z
- **Commit:** [`59c8552`](https://github.com/dhoard/client_java/commit/59c8552f3d67c06d82344383b45e07fea8ed88b9)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.66K | ± 1.63K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.30K | ± 111.22 | ops/s | 1.1x slower |
| prometheusAdd | 51.53K | ± 151.59 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.07K | ± 1.10K | ops/s | 1.3x slower |
| simpleclientInc | 6.79K | ± 35.17 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.70K | ± 23.40 | ops/s | 9.6x slower |
| simpleclientAdd | 6.26K | ± 222.05 | ops/s | 10x slower |
| openTelemetryInc | 1.34K | ± 153.72 | ops/s | 48x slower |
| openTelemetryAdd | 1.23K | ± 33.07 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.23K | ± 18.73 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.14K | ± 2.11K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 43.66 | ops/s | 1.4x slower |
| prometheusNative | 3.15K | ± 72.70 | ops/s | 1.9x slower |
| openTelemetryClassic | 649.43 | ± 17.05 | ops/s | 9.5x slower |
| openTelemetryExponential | 518.78 | ± 34.37 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 501.20K | ± 5.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.83K | ± 4.49K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.13K | ± 3.42K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.39K | ± 10.24K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49073.153   ± 1102.245  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1230.975     ± 33.067  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1343.458    ± 153.720  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1230.936     ± 18.731  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51528.366    ± 151.592  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64659.542   ± 1633.924  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57295.603    ± 111.218  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6259.923    ± 222.050  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6788.529     ± 35.174  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6700.945     ± 23.397  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        649.433     ± 17.046  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        518.776     ± 34.375  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6144.133   ± 2113.670  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3153.572     ± 72.700  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4467.498     ± 43.657  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477389.479  ± 10241.915  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483131.168   ± 3421.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492828.977   ± 4486.498  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501204.760   ± 5140.340  ops/s
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
