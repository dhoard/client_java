# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-16T04:16:02Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| codahaleIncNoLabels | 27.17K | ± 1.61K | ops/s | **fastest** |
| prometheusInc | 26.47K | ± 628.50 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.28K | ± 169.60 | ops/s | 1.0x slower |
| prometheusAdd | 25.00K | ± 828.19 | ops/s | 1.1x slower |
| openTelemetryIncNoLabels | 16.74K | ± 50.73 | ops/s | 1.6x slower |
| openTelemetryInc | 15.06K | ± 105.73 | ops/s | 1.8x slower |
| openTelemetryAdd | 13.08K | ± 81.16 | ops/s | 2.1x slower |
| simpleclientInc | 6.71K | ± 20.85 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 6.54K | ± 47.15 | ops/s | 4.2x slower |
| simpleclientAdd | 6.40K | ± 100.07 | ops/s | 4.2x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 6.63K | ± 92.24 | ops/s | **fastest** |
| simpleclient | 4.26K | ± 21.86 | ops/s | 1.6x slower |
| prometheusClassic | 3.05K | ± 1.62K | ops/s | 2.2x slower |
| prometheusClassicSingleThread | 2.85K | ± 87.29 | ops/s | 2.3x slower |
| prometheusNative | 1.90K | ± 249.30 | ops/s | 3.5x slower |
| openTelemetryClassic | 485.70 | ± 26.43 | ops/s | 14x slower |
| openTelemetryExponential | 477.00 | ± 48.84 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 17.82K | ± 30.20 | ops/s | **fastest** |
| openMetricsWriteToNull | 17.82K | ± 57.49 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 299.45K | ± 2.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 296.02K | ± 4.72K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 279.76K | ± 2.74K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 278.82K | ± 3.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27171.896   ± 1613.919  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13082.373     ± 81.159  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15057.007    ± 105.730  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16741.539     ± 50.734  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      24996.959    ± 828.188  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26474.908    ± 628.504  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26277.533    ± 169.597  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6403.413    ± 100.072  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6713.534     ± 20.847  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6543.151     ± 47.150  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        485.699     ± 26.429  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        477.004     ± 48.837  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3052.284   ± 1617.129  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6630.897     ± 92.244  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2853.147     ± 87.288  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1902.480    ± 249.296  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4262.469     ± 21.863  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17819.275     ± 57.486  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17820.407     ± 30.197  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     279761.294   ± 2736.675  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     278820.293   ± 3303.622  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     296021.026   ± 4720.084  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     299447.117   ± 2954.823  ops/s
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
