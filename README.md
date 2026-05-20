# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-20T07:13:56Z
- **Commit:** [`0bc0408`](https://github.com/dhoard/client_java/commit/0bc040814f37610ca3bb7b1f1474dbecdb20668d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.38K | ± 692.48 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.10K | ± 451.01 | ops/s | 1.2x slower |
| prometheusAdd | 48.38K | ± 175.57 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.94K | ± 88.29 | ops/s | 1.4x slower |
| simpleclientInc | 6.11K | ± 72.00 | ops/s | 9.9x slower |
| simpleclientAdd | 6.10K | ± 31.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.88K | ± 30.16 | ops/s | 10x slower |
| openTelemetryInc | 5.58K | ± 968.23 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 4.60K | ± 1.13K | ops/s | 13x slower |
| openTelemetryAdd | 3.46K | ± 151.65 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.71K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 97.68 | ops/s | 1.3x slower |
| prometheusNative | 2.91K | ± 243.67 | ops/s | 2.0x slower |
| openTelemetryClassic | 734.67 | ± 40.24 | ops/s | 7.8x slower |
| openTelemetryExponential | 580.71 | ± 9.73 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.40K | ± 283.57 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.30K | ± 185.29 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 585.95K | ± 4.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 569.29K | ± 7.41K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 542.59K | ± 5.09K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 524.57K | ± 12.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43943.998     ± 88.294  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3458.774    ± 151.647  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5583.605    ± 968.228  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4595.522   ± 1130.419  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48377.888    ± 175.569  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60378.770    ± 692.480  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51100.533    ± 451.008  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6096.285     ± 31.580  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6114.020     ± 71.999  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5879.692     ± 30.163  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        734.665     ± 40.243  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        580.708      ± 9.732  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5711.825   ± 1409.696  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2911.490    ± 243.674  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4557.743     ± 97.685  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27303.104    ± 185.290  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27399.165    ± 283.573  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524573.306  ± 12611.930  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542585.244   ± 5085.435  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     569290.550   ± 7414.387  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     585954.488   ± 4709.425  ops/s
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
