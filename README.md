# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-14T05:52:07Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.05K | ± 1.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.90K | ± 61.04 | ops/s | 1.2x slower |
| prometheusAdd | 48.47K | ± 99.86 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.47K | ± 151.30 | ops/s | 1.3x slower |
| simpleclientInc | 6.14K | ± 188.71 | ops/s | 9.6x slower |
| simpleclientAdd | 6.03K | ± 192.27 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.02K | ± 235.73 | ops/s | 9.8x slower |
| openTelemetryIncNoLabels | 1.40K | ± 176.65 | ops/s | 42x slower |
| openTelemetryAdd | 1.34K | ± 109.09 | ops/s | 44x slower |
| openTelemetryInc | 1.29K | ± 94.47 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.00K | ± 1.69K | ops/s | **fastest** |
| simpleclient | 4.21K | ± 21.44 | ops/s | 1.2x slower |
| prometheusNative | 2.62K | ± 27.27 | ops/s | 1.9x slower |
| openTelemetryClassic | 611.25 | ± 8.81 | ops/s | 8.2x slower |
| openTelemetryExponential | 505.24 | ± 21.28 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.08K | ± 10.13K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.79K | ± 6.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.22K | ± 4.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 530.24K | ± 5.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44466.011    ± 151.296  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1342.324    ± 109.089  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1285.008     ± 94.466  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1402.654    ± 176.654  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48469.219     ± 99.862  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59049.612   ± 1834.628  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50899.942     ± 61.036  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6026.875    ± 192.274  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6138.695    ± 188.706  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6016.810    ± 235.729  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        611.247      ± 8.806  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        505.236     ± 21.281  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5001.606   ± 1693.834  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2624.715     ± 27.271  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4209.898     ± 21.445  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     530239.134   ± 5934.902  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538222.750   ± 4076.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544786.876   ± 6211.049  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553080.954  ± 10130.689  ops/s
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
