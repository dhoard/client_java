# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-26T06:44:14Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.42K | ± 1.05K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.28K | ± 969.65 | ops/s | 1.2x slower |
| prometheusAdd | 51.23K | ± 215.53 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.64K | ± 704.17 | ops/s | 1.3x slower |
| simpleclientInc | 6.49K | ± 67.98 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 139.04 | ops/s | 10x slower |
| simpleclientAdd | 6.23K | ± 368.13 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.76K | ± 319.30 | ops/s | 17x slower |
| openTelemetryInc | 3.32K | ± 559.12 | ops/s | 20x slower |
| openTelemetryAdd | 3.27K | ± 179.58 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.42K | ± 288.10 | ops/s | **fastest** |
| prometheusClassic | 5.64K | ± 1.81K | ops/s | 2.2x slower |
| prometheusClassicSingleThread | 4.59K | ± 20.11 | ops/s | 2.7x slower |
| simpleclient | 4.35K | ± 15.24 | ops/s | 2.9x slower |
| prometheusNative | 2.80K | ± 326.48 | ops/s | 4.4x slower |
| openTelemetryClassic | 755.74 | ± 30.01 | ops/s | 16x slower |
| openTelemetryExponential | 595.65 | ± 84.69 | ops/s | 21x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.95K | ± 652.90 | ops/s | **fastest** |
| prometheusWriteToNull | 23.26K | ± 172.92 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 498.10K | ± 3.53K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.83K | ± 5.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.85K | ± 3.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.88K | ± 2.31K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50635.630    ± 704.175  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3270.949    ± 179.582  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3316.107    ± 559.124  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3757.320    ± 319.300  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51228.634    ± 215.532  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65423.487   ± 1053.216  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56283.988    ± 969.650  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6233.107    ± 368.130  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6491.492     ± 67.975  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6434.940    ± 139.044  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        755.737     ± 30.012  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        595.646     ± 84.689  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5642.796   ± 1810.073  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12419.602    ± 288.103  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4594.225     ± 20.114  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2798.609    ± 326.478  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4345.431     ± 15.243  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23949.598    ± 652.902  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23256.508    ± 172.919  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467878.357   ± 2308.278  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479852.357   ± 3075.890  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490827.251   ± 5663.280  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498102.540   ± 3533.886  ops/s
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
