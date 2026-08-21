# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-21T04:18:48Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusAdd | 35.97K | ± 400.42 | ops/s | **fastest** |
| prometheusInc | 35.00K | ± 759.42 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 34.95K | ± 1.39K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 34.38K | ± 1.46K | ops/s | 1.0x slower |
| openTelemetryIncNoLabels | 25.50K | ± 319.94 | ops/s | 1.4x slower |
| openTelemetryInc | 22.34K | ± 478.13 | ops/s | 1.6x slower |
| openTelemetryAdd | 18.82K | ± 1.23K | ops/s | 1.9x slower |
| simpleclientNoLabelsInc | 9.03K | ± 123.68 | ops/s | 4.0x slower |
| simpleclientInc | 9.01K | ± 240.25 | ops/s | 4.0x slower |
| simpleclientAdd | 8.68K | ± 245.26 | ops/s | 4.1x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 9.19K | ± 220.01 | ops/s | **fastest** |
| simpleclient | 5.94K | ± 167.01 | ops/s | 1.5x slower |
| prometheusClassicSingleThread | 4.57K | ± 78.80 | ops/s | 2.0x slower |
| prometheusClassic | 3.00K | ± 572.78 | ops/s | 3.1x slower |
| prometheusNative | 2.32K | ± 518.83 | ops/s | 4.0x slower |
| openTelemetryClassic | 493.16 | ± 5.49 | ops/s | 19x slower |
| openTelemetryExponential | 475.80 | ± 10.60 | ops/s | 19x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.82K | ± 841.48 | ops/s | **fastest** |
| prometheusWriteToNull | 24.76K | ± 1.09K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 351.23K | ± 7.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 335.98K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 326.75K | ± 8.92K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 326.73K | ± 3.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      34381.416   ± 1463.740  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      18816.885   ± 1228.363  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      22341.173    ± 478.133  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      25503.566    ± 319.943  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      35972.897    ± 400.422  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      34999.992    ± 759.419  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      34951.708   ± 1391.478  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8677.852    ± 245.259  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9014.223    ± 240.245  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9031.447    ± 123.676  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        493.157      ± 5.487  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        475.797     ± 10.596  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3004.326    ± 572.784  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       9186.226    ± 220.014  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4565.927     ± 78.797  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2324.972    ± 518.831  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5941.121    ± 167.011  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24821.738    ± 841.483  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24758.153   ± 1088.695  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     326753.891   ± 8916.857  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     326726.978   ± 3599.760  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     335981.086   ± 2775.210  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     351228.401   ± 7319.134  ops/s
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
