# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-12T05:19:17Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.24K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.84K | ± 412.65 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 89.93 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.79K | ± 1.56K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.17K | ± 311.59 | ops/s | 3.6x slower |
| openTelemetryInc | 15.11K | ± 87.13 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.98K | ± 72.61 | ops/s | 5.0x slower |
| simpleclientInc | 6.55K | ± 45.03 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.34K | ± 253.35 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 258.04 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.26K | ± 76.42 | ops/s | **fastest** |
| prometheusClassic | 6.90K | ± 2.45K | ops/s | 1.8x slower |
| prometheusClassicSingleThread | 4.52K | ± 97.21 | ops/s | 2.7x slower |
| simpleclient | 4.39K | ± 60.12 | ops/s | 2.8x slower |
| prometheusNative | 2.70K | ± 241.44 | ops/s | 4.5x slower |
| openTelemetryExponential | 802.09 | ± 101.32 | ops/s | 15x slower |
| openTelemetryClassic | 749.59 | ± 13.67 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.82K | ± 1.15K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.79K | ± 613.86 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 515.44K | ± 4.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.91K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 492.64K | ± 2.62K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.50K | ± 2.33K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48788.884   ± 1558.757  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12975.434     ± 72.609  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15114.790     ± 87.129  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18169.032    ± 311.588  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51302.200     ± 89.926  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65237.511   ± 1227.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56837.158    ± 412.646  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6335.798    ± 258.042  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6553.311     ± 45.031  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6340.008    ± 253.351  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.587     ± 13.672  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        802.090    ± 101.317  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6903.939   ± 2454.202  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12256.633     ± 76.422  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4520.469     ± 97.213  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2702.670    ± 241.435  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4391.142     ± 60.120  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23787.223    ± 613.860  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23824.390   ± 1154.243  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483496.585   ± 2333.201  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492642.416   ± 2618.652  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505909.030   ± 2783.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515444.692   ± 4858.494  ops/s
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
