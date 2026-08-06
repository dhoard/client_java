# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-06T06:18:23Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.91K | ± 484.43 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.17K | ± 950.91 | ops/s | 1.2x slower |
| prometheusAdd | 51.57K | ± 144.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.25K | ± 1.50K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 17.52K | ± 1.63K | ops/s | 3.8x slower |
| openTelemetryInc | 15.05K | ± 225.90 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.91K | ± 184.79 | ops/s | 5.1x slower |
| simpleclientInc | 6.57K | ± 41.05 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 176.94 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 8.59 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.30K | ± 25.79 | ops/s | **fastest** |
| prometheusClassic | 6.16K | ± 1.43K | ops/s | 2.0x slower |
| prometheusClassicSingleThread | 4.53K | ± 26.78 | ops/s | 2.7x slower |
| simpleclient | 4.41K | ± 46.03 | ops/s | 2.8x slower |
| prometheusNative | 3.20K | ± 65.11 | ops/s | 3.8x slower |
| openTelemetryExponential | 840.72 | ± 119.35 | ops/s | 15x slower |
| openTelemetryClassic | 808.58 | ± 65.66 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.68K | ± 705.58 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.33K | ± 1.20K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 500.94K | ± 2.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.71K | ± 8.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.54K | ± 5.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.06K | ± 2.54K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49250.061   ± 1501.872  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12909.628    ± 184.792  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15047.376    ± 225.900  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17518.875   ± 1625.163  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51569.795    ± 144.619  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65909.273    ± 484.435  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56168.532    ± 950.907  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6336.670    ± 176.943  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6569.024     ± 41.047  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6334.735      ± 8.591  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        808.585     ± 65.657  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        840.720    ± 119.353  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6157.113   ± 1425.719  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12302.620     ± 25.789  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4525.687     ± 26.781  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3198.108     ± 65.108  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4410.849     ± 46.031  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23332.739   ± 1198.584  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23676.402    ± 705.579  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481057.844   ± 2540.354  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482535.832   ± 5484.702  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499712.404   ± 8513.571  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500935.417   ± 2677.877  ops/s
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
