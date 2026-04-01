# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-01T05:54:10Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.10K | ± 1.39K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.81K | ± 1.15K | ops/s | 1.2x slower |
| prometheusAdd | 51.33K | ± 65.45 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.51K | ± 1.77K | ops/s | 1.3x slower |
| simpleclientInc | 6.50K | ± 192.63 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.48K | ± 194.47 | ops/s | 10x slower |
| simpleclientAdd | 6.09K | ± 339.65 | ops/s | 11x slower |
| openTelemetryInc | 1.50K | ± 194.06 | ops/s | 43x slower |
| openTelemetryAdd | 1.37K | ± 199.51 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.22K | ± 15.71 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.80K | ± 877.60 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 78.78 | ops/s | 1.1x slower |
| prometheusNative | 3.05K | ± 280.41 | ops/s | 1.6x slower |
| openTelemetryClassic | 670.49 | ± 43.66 | ops/s | 7.2x slower |
| openTelemetryExponential | 581.31 | ± 16.66 | ops/s | 8.3x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.95K | ± 4.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.11K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.75K | ± 5.05K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.68K | ± 4.32K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49506.209   ± 1771.460  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1374.351    ± 199.507  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1499.394    ± 194.058  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1222.641     ± 15.711  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51332.148     ± 65.454  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65096.057   ± 1389.790  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55807.789   ± 1152.156  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6094.891    ± 339.650  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6504.660    ± 192.628  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6477.329    ± 194.471  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        670.495     ± 43.663  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        581.305     ± 16.657  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4804.061    ± 877.595  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3053.860    ± 280.408  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4436.552     ± 78.779  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473681.282   ± 4318.824  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485749.724   ± 5050.113  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494107.431   ± 2782.316  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499949.616   ± 4904.900  ops/s
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
