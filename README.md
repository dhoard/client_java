# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-15T05:27:03Z
- **Commit:** [`229e2e0`](https://github.com/dhoard/client_java/commit/229e2e003bd639f3744566940f503d05e8b9ba18)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.09K | ± 1.86K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.36K | ± 1.11K | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 412.46 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.69K | ± 2.09K | ops/s | 1.4x slower |
| simpleclientInc | 6.76K | ± 30.72 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.61K | ± 128.29 | ops/s | 9.9x slower |
| simpleclientAdd | 6.54K | ± 26.78 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.51K | ± 239.70 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.31K | ± 20.79 | ops/s | 50x slower |
| openTelemetryInc | 1.22K | ± 40.60 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.39K | ± 1.78K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 13.01 | ops/s | 1.2x slower |
| prometheusNative | 2.91K | ± 365.29 | ops/s | 1.9x slower |
| openTelemetryClassic | 701.85 | ± 71.53 | ops/s | 7.7x slower |
| openTelemetryExponential | 566.70 | ± 20.26 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 506.99K | ± 4.03K | ops/s | **fastest** |
| openMetricsWriteToNull | 493.63K | ± 2.18K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.83K | ± 2.14K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 478.32K | ± 32.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47689.589   ± 2092.780  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1505.065    ± 239.704  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1219.795     ± 40.598  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1312.065     ± 20.788  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51290.836    ± 412.461  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65090.275   ± 1857.685  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56363.723   ± 1112.589  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6537.067     ± 26.784  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6764.348     ± 30.716  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6606.383    ± 128.294  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.845     ± 71.527  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.698     ± 20.260  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5392.806   ± 1781.284  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2907.034    ± 365.293  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4566.645     ± 13.015  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485827.168   ± 2137.069  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     493625.686   ± 2181.108  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     478316.604  ± 32803.726  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506989.050   ± 4031.693  ops/s
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
