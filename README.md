# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-20T05:19:23Z
- **Commit:** [`3524bcf`](https://github.com/dhoard/client_java/commit/3524bcfd17124a9d34e8f4f2aa5d530e0db14fdd)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.47K | ± 290.75 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.25K | ± 168.91 | ops/s | 1.2x slower |
| prometheusAdd | 51.11K | ± 538.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.11K | ± 1.13K | ops/s | 1.4x slower |
| simpleclientInc | 6.61K | ± 144.53 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.57K | ± 213.93 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 20.15 | ops/s | 11x slower |
| openTelemetryAdd | 1.29K | ± 53.97 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.23K | ± 30.86 | ops/s | 54x slower |
| openTelemetryInc | 1.21K | ± 47.49 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.47K | ± 911.80 | ops/s | **fastest** |
| simpleclient | 4.49K | ± 112.42 | ops/s | 1.4x slower |
| prometheusNative | 3.16K | ± 90.97 | ops/s | 2.0x slower |
| openTelemetryClassic | 693.00 | ± 18.13 | ops/s | 9.3x slower |
| openTelemetryExponential | 544.05 | ± 6.14 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 491.73K | ± 4.08K | ops/s | **fastest** |
| prometheusWriteToByteArray | 486.67K | ± 2.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.97K | ± 2.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.24K | ± 9.85K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49107.188   ± 1129.831  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1287.192     ± 53.968  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1214.821     ± 47.492  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1228.743     ± 30.858  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51110.750    ± 538.062  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66465.876    ± 290.751  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57252.040    ± 168.905  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6238.709     ± 20.147  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6605.707    ± 144.528  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6572.488    ± 213.929  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.998     ± 18.128  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.055      ± 6.139  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6472.392    ± 911.802  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3164.752     ± 90.971  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4488.208    ± 112.420  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468244.897   ± 9849.596  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473965.268   ± 2628.867  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     486674.564   ± 2468.317  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     491730.978   ± 4079.307  ops/s
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
