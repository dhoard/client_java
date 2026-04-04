# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-04T05:22:06Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.27K | ± 1.53K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 79.66 | ops/s | 1.1x slower |
| prometheusAdd | 50.37K | ± 1.12K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.15K | ± 1.44K | ops/s | 1.3x slower |
| simpleclientAdd | 6.48K | ± 45.49 | ops/s | 10x slower |
| simpleclientInc | 6.45K | ± 116.90 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 146.28 | ops/s | 10x slower |
| openTelemetryInc | 1.30K | ± 180.98 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.27K | ± 86.92 | ops/s | 51x slower |
| openTelemetryAdd | 1.27K | ± 56.42 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.42K | ± 2.67K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 55.30 | ops/s | 1.4x slower |
| prometheusNative | 2.53K | ± 87.24 | ops/s | 2.5x slower |
| openTelemetryClassic | 703.75 | ± 18.92 | ops/s | 9.1x slower |
| openTelemetryExponential | 530.05 | ± 23.08 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.02K | ± 5.80K | ops/s | **fastest** |
| openMetricsWriteToNull | 487.08K | ± 2.73K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 485.00K | ± 9.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.57K | ± 4.06K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49154.295   ± 1435.678  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1272.638     ± 56.420  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1300.134    ± 180.983  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1274.908     ± 86.917  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50370.871   ± 1115.514  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65268.222   ± 1525.741  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57205.649     ± 79.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6477.909     ± 45.485  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6449.093    ± 116.904  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6434.953    ± 146.276  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.754     ± 18.921  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.055     ± 23.080  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6420.620   ± 2668.051  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2527.445     ± 87.242  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.084     ± 55.301  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484573.586   ± 4056.065  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487082.966   ± 2726.664  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484996.048   ± 9155.813  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493015.650   ± 5798.589  ops/s
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
