# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-07T05:39:48Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.53K | ± 103.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.22K | ± 215.99 | ops/s | 1.2x slower |
| prometheusAdd | 51.15K | ± 346.72 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.60K | ± 412.07 | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 245.12 | ops/s | 10x slower |
| simpleclientAdd | 6.48K | ± 26.31 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.38K | ± 183.91 | ops/s | 10x slower |
| openTelemetryAdd | 1.33K | ± 63.21 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.32K | ± 155.27 | ops/s | 50x slower |
| openTelemetryInc | 1.27K | ± 58.51 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.34K | ± 2.08K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 101.09 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 311.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 699.79 | ± 31.18 | ops/s | 7.6x slower |
| openTelemetryExponential | 551.73 | ± 27.29 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.44K | ± 2.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.23K | ± 4.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.78K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.79K | ± 3.55K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50597.758    ± 412.067  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1329.629     ± 63.206  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1272.222     ± 58.513  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1318.397    ± 155.270  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51150.931    ± 346.716  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66528.489    ± 103.560  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57217.908    ± 215.991  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6478.678     ± 26.314  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6550.413    ± 245.118  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6380.730    ± 183.914  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        699.791     ± 31.182  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.733     ± 27.290  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5341.854   ± 2082.868  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3000.939    ± 311.696  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.682    ± 101.095  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480786.132   ± 3553.796  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482778.374   ± 3896.807  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491230.239   ± 4884.907  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494442.272   ± 2264.111  ops/s
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
