# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-23T05:57:49Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1011-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.29K | ± 616.33 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.82K | ± 509.92 | ops/s | 1.2x slower |
| prometheusAdd | 51.68K | ± 106.65 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.47K | ± 540.14 | ops/s | 1.3x slower |
| simpleclientInc | 6.60K | ± 160.93 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 178.81 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 237.53 | ops/s | 11x slower |
| openTelemetryAdd | 1.55K | ± 233.47 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.28K | ± 87.89 | ops/s | 52x slower |
| openTelemetryInc | 1.24K | ± 4.78 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.50K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 17.33 | ops/s | 1.3x slower |
| prometheusNative | 2.78K | ± 336.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 695.38 | ± 29.59 | ops/s | 7.9x slower |
| openTelemetryExponential | 560.23 | ± 10.52 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.24K | ± 6.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 470.47K | ± 7.59K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 463.21K | ± 3.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 455.50K | ± 3.12K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50474.440    ± 540.137  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1548.176    ± 233.475  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1238.899      ± 4.777  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1279.005     ± 87.892  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51684.789    ± 106.650  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66288.856    ± 616.334  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56821.693    ± 509.923  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6294.289    ± 237.529  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6600.185    ± 160.930  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6393.229    ± 178.806  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.385     ± 29.585  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.233     ± 10.517  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5501.247   ± 1422.345  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2783.070    ± 336.004  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4381.928     ± 17.331  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     455499.023   ± 3117.306  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     463205.510   ± 3018.080  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     470466.649   ± 7592.073  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484244.735   ± 6159.299  ops/s
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
