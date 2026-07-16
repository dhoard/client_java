# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-16T06:05:31Z
- **Commit:** [`be2bc20`](https://github.com/dhoard/client_java/commit/be2bc20fdf941be85a0ad020f5f405af623a7883)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.59K | ± 1.01K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.76K | ± 288.63 | ops/s | 1.1x slower |
| prometheusAdd | 50.72K | ± 233.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.19K | ± 645.67 | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 11.16 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.29K | ± 122.93 | ops/s | 10x slower |
| simpleclientAdd | 6.15K | ± 345.54 | ops/s | 11x slower |
| openTelemetryInc | 3.42K | ± 396.56 | ops/s | 19x slower |
| openTelemetryAdd | 3.38K | ± 326.25 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.12K | ± 269.43 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 5.63K | ± 1.48K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 57.79 | ops/s | 1.3x slower |
| prometheusNative | 3.00K | ± 387.71 | ops/s | 1.9x slower |
| openTelemetryClassic | 750.36 | ± 36.41 | ops/s | 7.5x slower |
| openTelemetryExponential | 568.94 | ± 16.90 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.68K | ± 975.67 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.14K | ± 1.15K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 512.19K | ± 4.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.58K | ± 6.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.43K | ± 3.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.54K | ± 6.56K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49192.933    ± 645.675  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3380.733    ± 326.250  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3418.980    ± 396.561  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3122.131    ± 269.433  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50724.985    ± 233.678  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64586.035   ± 1014.685  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56763.291    ± 288.632  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6149.966    ± 345.536  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.776     ± 11.158  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6288.797    ± 122.926  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.363     ± 36.408  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        568.944     ± 16.898  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5627.276   ± 1479.018  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3003.478    ± 387.707  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4413.911     ± 57.788  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23138.581   ± 1145.830  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23678.653    ± 975.670  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481544.202   ± 6557.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489429.023   ± 3878.322  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497581.119   ± 6196.778  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512187.015   ± 4711.046  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
