# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-28T06:16:59Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.34K | ± 766.80 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.11K | ± 913.35 | ops/s | 1.2x slower |
| prometheusAdd | 48.03K | ± 965.16 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.09K | ± 309.74 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 6.50K | ± 314.76 | ops/s | 9.3x slower |
| simpleclientInc | 6.13K | ± 47.37 | ops/s | 9.8x slower |
| simpleclientAdd | 5.98K | ± 117.66 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.89K | ± 5.94 | ops/s | 10x slower |
| openTelemetryInc | 5.27K | ± 1.37K | ops/s | 11x slower |
| openTelemetryAdd | 4.59K | ± 916.67 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.62K | ± 20.31 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.95K | ± 15.67 | ops/s | 2.5x slower |
| prometheusClassic | 4.59K | ± 1.11K | ops/s | 3.2x slower |
| simpleclient | 4.51K | ± 34.16 | ops/s | 3.2x slower |
| prometheusNative | 2.92K | ± 245.79 | ops/s | 5.0x slower |
| openTelemetryClassic | 704.26 | ± 36.74 | ops/s | 21x slower |
| openTelemetryExponential | 565.67 | ± 26.00 | ops/s | 26x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 27.33K | ± 273.77 | ops/s | **fastest** |
| prometheusWriteToNull | 27.24K | ± 598.19 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 588.75K | ± 9.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.12K | ± 12.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.83K | ± 2.23K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.04K | ± 5.41K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44087.492    ± 309.740  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4593.785    ± 916.674  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5267.353   ± 1365.789  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6502.588    ± 314.759  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48029.756    ± 965.161  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60342.732    ± 766.796  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52109.207    ± 913.352  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5977.420    ± 117.657  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6127.868     ± 47.371  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5894.352      ± 5.941  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.265     ± 36.739  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.666     ± 26.004  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4587.454   ± 1110.234  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14618.004     ± 20.311  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5945.850     ± 15.673  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2921.293    ± 245.793  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4514.615     ± 34.156  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27328.577    ± 273.770  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27239.520    ± 598.189  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532039.109   ± 5407.777  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548831.747   ± 2227.853  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568119.481  ± 12426.370  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     588747.577   ± 9445.483  ops/s
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
