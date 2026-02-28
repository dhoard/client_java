# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-28T05:01:40Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.16K | ± 353.14 | ops/s | **fastest** |
| prometheusInc | 30.80K | ± 1.18K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.27K | ± 82.58 | ops/s | 1.1x slower |
| prometheusAdd | 28.42K | ± 94.64 | ops/s | 1.1x slower |
| simpleclientInc | 7.16K | ± 149.48 | ops/s | 4.4x slower |
| simpleclientAdd | 6.77K | ± 123.67 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.72K | ± 260.96 | ops/s | 4.6x slower |
| openTelemetryIncNoLabels | 1.39K | ± 65.64 | ops/s | 22x slower |
| openTelemetryInc | 1.36K | ± 72.19 | ops/s | 23x slower |
| openTelemetryAdd | 1.33K | ± 74.34 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.55K | ± 48.23 | ops/s | **fastest** |
| prometheusClassic | 3.33K | ± 1.34K | ops/s | 1.4x slower |
| prometheusNative | 2.21K | ± 228.77 | ops/s | 2.1x slower |
| openTelemetryClassic | 528.55 | ± 13.59 | ops/s | 8.6x slower |
| openTelemetryExponential | 392.01 | ± 18.42 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 314.43K | ± 1.51K | ops/s | **fastest** |
| prometheusWriteToNull | 313.42K | ± 3.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.88K | ± 1.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.43K | ± 1.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29268.248     ± 82.585  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1334.511     ± 74.344  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1357.975     ± 72.189  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1387.421     ± 65.637  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28415.637     ± 94.641  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30797.958   ± 1184.151  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31157.294    ± 353.143  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6770.189    ± 123.671  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7158.245    ± 149.477  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6717.044    ± 260.957  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        528.555     ± 13.594  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        392.010     ± 18.420  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3327.219   ± 1341.161  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2214.346    ± 228.771  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.772     ± 48.229  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294428.438   ± 1227.662  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296876.096   ± 1629.349  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     314430.968   ± 1513.277  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     313415.875   ± 3154.582  ops/s
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
