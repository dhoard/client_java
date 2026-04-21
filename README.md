# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-21T05:55:11Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.30K | ± 772.01 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.17K | ± 393.78 | ops/s | 1.2x slower |
| prometheusAdd | 48.08K | ± 630.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.57K | ± 310.98 | ops/s | 1.4x slower |
| simpleclientInc | 6.25K | ± 140.68 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.24K | ± 28.91 | ops/s | 9.7x slower |
| simpleclientAdd | 5.87K | ± 228.42 | ops/s | 10x slower |
| openTelemetryAdd | 1.38K | ± 73.09 | ops/s | 44x slower |
| openTelemetryInc | 1.30K | ± 13.96 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.26K | ± 57.30 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.56K | ± 1.51K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 69.26 | ops/s | 1.3x slower |
| prometheusNative | 2.95K | ± 238.18 | ops/s | 1.9x slower |
| openTelemetryClassic | 598.99 | ± 4.60 | ops/s | 9.3x slower |
| openTelemetryExponential | 495.26 | ± 14.94 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 538.11K | ± 6.47K | ops/s | **fastest** |
| prometheusWriteToByteArray | 526.52K | ± 5.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 520.25K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 507.80K | ± 5.68K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44567.478    ± 310.981  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1378.559     ± 73.086  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1301.394     ± 13.965  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1262.286     ± 57.300  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48079.960    ± 630.890  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60295.307    ± 772.009  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51169.578    ± 393.781  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5874.056    ± 228.419  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6247.357    ± 140.675  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6235.945     ± 28.910  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        598.988      ± 4.596  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        495.258     ± 14.936  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5559.889   ± 1513.729  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2948.917    ± 238.180  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4345.733     ± 69.265  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     507795.975   ± 5680.768  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     520254.534   ± 2121.015  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     526524.945   ± 5122.405  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     538109.940   ± 6471.087  ops/s
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
