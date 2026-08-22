# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-22T04:09:55Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 74.85K | ± 2.91K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.53K | ± 655.82 | ops/s | 1.1x slower |
| prometheusAdd | 62.51K | ± 1.74K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.74K | ± 755.62 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 21.87K | ± 320.39 | ops/s | 3.4x slower |
| openTelemetryInc | 17.55K | ± 439.02 | ops/s | 4.3x slower |
| openTelemetryAdd | 15.73K | ± 46.96 | ops/s | 4.8x slower |
| simpleclientInc | 7.96K | ± 77.93 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 7.76K | ± 218.82 | ops/s | 9.6x slower |
| simpleclientAdd | 7.61K | ± 410.30 | ops/s | 9.8x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 18.13K | ± 61.03 | ops/s | **fastest** |
| prometheusClassic | 9.06K | ± 654.59 | ops/s | 2.0x slower |
| prometheusClassicSingleThread | 7.49K | ± 22.21 | ops/s | 2.4x slower |
| simpleclient | 5.87K | ± 118.98 | ops/s | 3.1x slower |
| prometheusNative | 3.57K | ± 428.66 | ops/s | 5.1x slower |
| openTelemetryClassic | 954.89 | ± 9.65 | ops/s | 19x slower |
| openTelemetryExponential | 781.05 | ± 24.61 | ops/s | 23x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.43K | ± 140.65 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.38K | ± 238.04 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 703.61K | ± 6.70K | ops/s | **fastest** |
| prometheusWriteToByteArray | 683.92K | ± 5.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 661.38K | ± 5.16K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 646.71K | ± 5.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57739.658    ± 755.622  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15732.319     ± 46.960  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17551.046    ± 439.023  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21874.520    ± 320.392  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62510.884   ± 1735.088  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      74845.283   ± 2906.262  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66532.205    ± 655.816  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7607.477    ± 410.299  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7959.532     ± 77.926  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7764.587    ± 218.822  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        954.885      ± 9.654  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        781.046     ± 24.608  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9056.256    ± 654.591  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18132.516     ± 61.030  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7492.364     ± 22.215  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3565.194    ± 428.660  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5867.467    ± 118.978  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35384.512    ± 238.037  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35427.779    ± 140.653  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     646706.653   ± 5195.054  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     661377.142   ± 5156.667  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     683921.988   ± 5274.847  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     703611.714   ± 6702.721  ops/s
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
