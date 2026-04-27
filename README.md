# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-27T06:13:46Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.65K | ± 2.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.88K | ± 899.91 | ops/s | 1.1x slower |
| prometheusAdd | 47.72K | ± 295.19 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.88K | ± 1.46K | ops/s | 1.3x slower |
| simpleclientInc | 6.26K | ± 75.86 | ops/s | 9.2x slower |
| simpleclientNoLabelsInc | 5.99K | ± 233.90 | ops/s | 9.6x slower |
| simpleclientAdd | 5.91K | ± 283.99 | ops/s | 9.7x slower |
| openTelemetryAdd | 1.33K | ± 98.22 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 126.21 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.29K | ± 99.51 | ops/s | 45x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.42K | ± 541.37 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 75.58 | ops/s | 1.0x slower |
| prometheusNative | 2.80K | ± 259.17 | ops/s | 1.6x slower |
| openTelemetryClassic | 598.86 | ± 20.30 | ops/s | 7.4x slower |
| openTelemetryExponential | 512.77 | ± 25.10 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.33K | ± 9.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.65K | ± 2.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 535.55K | ± 4.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 525.78K | ± 4.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42878.444   ± 1462.665  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1326.399     ± 98.221  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1306.072    ± 126.207  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1289.058     ± 99.514  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47719.957    ± 295.192  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57645.104   ± 2883.877  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50877.261    ± 899.907  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5913.674    ± 283.986  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6261.341     ± 75.856  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5986.795    ± 233.896  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        598.856     ± 20.296  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        512.771     ± 25.105  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4415.916    ± 541.370  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2804.203    ± 259.168  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4343.804     ± 75.583  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525783.440   ± 4747.757  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     535554.910   ± 4934.207  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547650.745   ± 2765.602  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556333.216   ± 9579.333  ops/s
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
