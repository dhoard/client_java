# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-05T06:07:29Z
- **Commit:** [`0d33b2a`](https://github.com/dhoard/client_java/commit/0d33b2a21208a58f0c67c0e9a9b662044ded45d2)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.39K | ± 1.14K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.60K | ± 518.83 | ops/s | 1.2x slower |
| prometheusAdd | 48.10K | ± 288.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 40.48K | ± 5.63K | ops/s | 1.5x slower |
| simpleclientInc | 6.21K | ± 120.46 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.10K | ± 233.09 | ops/s | 9.9x slower |
| simpleclientAdd | 5.83K | ± 12.76 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.27K | ± 673.40 | ops/s | 11x slower |
| openTelemetryInc | 5.07K | ± 836.90 | ops/s | 12x slower |
| openTelemetryAdd | 4.14K | ± 892.72 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.22K | ± 519.36 | ops/s | **fastest** |
| simpleclient | 4.14K | ± 71.06 | ops/s | 1.0x slower |
| prometheusNative | 3.12K | ± 117.37 | ops/s | 1.4x slower |
| openTelemetryClassic | 712.60 | ± 28.80 | ops/s | 5.9x slower |
| openTelemetryExponential | 535.67 | ± 11.01 | ops/s | 7.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.05K | ± 8.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 548.98K | ± 4.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.02K | ± 4.33K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 522.60K | ± 7.90K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40481.910   ± 5629.922  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4139.865    ± 892.722  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5066.250    ± 836.896  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5270.533    ± 673.405  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48104.643    ± 288.841  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60393.228   ± 1138.920  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51598.303    ± 518.831  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5829.679     ± 12.765  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6208.319    ± 120.460  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6102.767    ± 233.094  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        712.603     ± 28.800  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        535.669     ± 11.008  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4222.910    ± 519.360  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3120.983    ± 117.368  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4143.946     ± 71.063  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522602.424   ± 7895.279  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538017.988   ± 4327.795  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548976.181   ± 4386.031  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555054.478   ± 8052.868  ops/s
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
