# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-30T06:36:19Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.53K | ± 39.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 29.73K | ± 868.27 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.98K | ± 690.52 | ops/s | 1.1x slower |
| prometheusAdd | 28.27K | ± 553.23 | ops/s | 1.1x slower |
| simpleclientInc | 6.99K | ± 48.79 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.63K | ± 262.34 | ops/s | 4.8x slower |
| simpleclientAdd | 6.57K | ± 194.87 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 1.34K | ± 65.91 | ops/s | 24x slower |
| openTelemetryInc | 1.31K | ± 89.45 | ops/s | 24x slower |
| openTelemetryAdd | 1.27K | ± 117.57 | ops/s | 25x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.56K | ± 45.74 | ops/s | **fastest** |
| prometheusClassic | 2.82K | ± 470.32 | ops/s | 1.6x slower |
| prometheusNative | 2.16K | ± 195.23 | ops/s | 2.1x slower |
| openTelemetryClassic | 514.18 | ± 41.09 | ops/s | 8.9x slower |
| openTelemetryExponential | 378.76 | ± 13.52 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 311.97K | ± 992.77 | ops/s | **fastest** |
| prometheusWriteToByteArray | 307.64K | ± 1.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 293.78K | ± 2.31K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 289.70K | ± 1.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28979.852    ± 690.524  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1271.998    ± 117.569  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1309.178     ± 89.445  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1336.075     ± 65.907  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28266.886    ± 553.228  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31526.532     ± 39.123  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29725.775    ± 868.272  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6572.105    ± 194.868  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6985.143     ± 48.787  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6629.362    ± 262.343  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        514.177     ± 41.085  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        378.759     ± 13.517  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2822.281    ± 470.315  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2158.341    ± 195.234  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4563.834     ± 45.739  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     289702.572   ± 1412.271  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     293779.880   ± 2313.486  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     307640.312   ± 1991.301  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     311973.947    ± 992.766  ops/s
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
