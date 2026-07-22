# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-22T06:21:15Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 58.96K | ± 1.44K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.11K | ± 495.97 | ops/s | 1.2x slower |
| prometheusAdd | 48.16K | ± 373.66 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.91K | ± 1.35K | ops/s | 1.3x slower |
| simpleclientInc | 6.09K | ± 10.84 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.91K | ± 19.00 | ops/s | 10.0x slower |
| simpleclientAdd | 5.79K | ± 257.13 | ops/s | 10x slower |
| openTelemetryInc | 4.62K | ± 1.43K | ops/s | 13x slower |
| openTelemetryAdd | 4.15K | ± 864.48 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.92K | ± 235.54 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.32K | ± 317.15 | ops/s | **fastest** |
| prometheusClassic | 7.51K | ± 164.64 | ops/s | 1.9x slower |
| prometheusClassicSingleThread | 5.95K | ± 15.98 | ops/s | 2.4x slower |
| simpleclient | 4.54K | ± 119.89 | ops/s | 3.2x slower |
| prometheusNative | 3.18K | ± 49.40 | ops/s | 4.5x slower |
| openTelemetryClassic | 745.07 | ± 16.74 | ops/s | 19x slower |
| openTelemetryExponential | 555.45 | ± 13.40 | ops/s | 26x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 27.21K | ± 399.92 | ops/s | **fastest** |
| prometheusWriteToNull | 27.14K | ± 553.59 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 579.48K | ± 3.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 567.05K | ± 3.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.81K | ± 18.87K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.81K | ± 3.38K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44912.234   ± 1353.144  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4150.830    ± 864.479  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4623.172   ± 1430.604  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3919.917    ± 235.543  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48158.630    ± 373.660  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58960.221   ± 1438.386  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51111.353    ± 495.973  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5792.947    ± 257.132  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6094.930     ± 10.840  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5911.015     ± 19.002  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        745.070     ± 16.738  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.454     ± 13.395  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7511.754    ± 164.641  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14318.419    ± 317.148  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5953.800     ± 15.985  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3175.398     ± 49.398  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4539.027    ± 119.890  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27210.327    ± 399.922  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27136.816    ± 553.592  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532812.431   ± 3382.079  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538809.630  ± 18867.129  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     567045.890   ± 3226.937  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579477.939   ± 3213.520  ops/s
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
