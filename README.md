# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-20T06:04:34Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.50K | ± 2.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.41K | ± 1.40K | ops/s | 1.1x slower |
| prometheusAdd | 50.09K | ± 1.05K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.32K | ± 1.66K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 14.83 | ops/s | 9.6x slower |
| simpleclientAdd | 6.32K | ± 243.21 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 111.23 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 210.04 | ops/s | 46x slower |
| openTelemetryInc | 1.39K | ± 140.42 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.17K | ± 34.86 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.53K | ± 939.30 | ops/s | **fastest** |
| simpleclient | 4.36K | ± 133.03 | ops/s | 1.5x slower |
| prometheusNative | 2.93K | ± 253.61 | ops/s | 2.2x slower |
| openTelemetryClassic | 703.32 | ± 27.54 | ops/s | 9.3x slower |
| openTelemetryExponential | 561.66 | ± 31.44 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.95K | ± 3.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.58K | ± 1.79K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.94K | ± 7.31K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.53K | ± 5.30K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48315.447   ± 1656.806  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1416.770    ± 210.037  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1386.525    ± 140.416  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1170.886     ± 34.856  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50094.362   ± 1046.144  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64503.123   ± 2051.330  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56412.968   ± 1396.404  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6316.789    ± 243.215  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6696.027     ± 14.832  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6309.439    ± 111.228  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.316     ± 27.539  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        561.661     ± 31.437  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6532.534    ± 939.295  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2934.898    ± 253.609  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4361.551    ± 133.033  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482531.363   ± 5300.865  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485937.805   ± 7313.026  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490584.226   ± 1793.532  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493948.264   ± 3771.336  ops/s
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
