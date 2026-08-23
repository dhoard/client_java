# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-23T04:18:50Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.57K | ± 1.68K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.22K | ± 1.03K | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 128.68 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.89K | ± 1.55K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.45K | ± 169.55 | ops/s | 3.6x slower |
| openTelemetryInc | 14.79K | ± 309.30 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.62K | ± 236.80 | ops/s | 5.2x slower |
| simpleclientInc | 6.53K | ± 36.12 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 31.96 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 182.54 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.30K | ± 33.15 | ops/s | **fastest** |
| prometheusClassic | 5.73K | ± 607.77 | ops/s | 2.1x slower |
| simpleclient | 4.50K | ± 40.84 | ops/s | 2.7x slower |
| prometheusClassicSingleThread | 4.47K | ± 145.77 | ops/s | 2.7x slower |
| prometheusNative | 3.00K | ± 235.07 | ops/s | 4.1x slower |
| openTelemetryClassic | 902.34 | ± 59.76 | ops/s | 14x slower |
| openTelemetryExponential | 719.51 | ± 68.47 | ops/s | 17x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.59K | ± 531.80 | ops/s | **fastest** |
| prometheusWriteToNull | 23.17K | ± 624.40 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 502.92K | ± 3.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.02K | ± 3.90K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.39K | ± 2.37K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.85K | ± 2.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48887.663   ± 1548.054  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12622.249    ± 236.800  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14787.316    ± 309.298  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18454.023    ± 169.550  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51596.328    ± 128.683  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65572.991   ± 1682.681  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56221.557   ± 1034.573  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6210.949    ± 182.540  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6531.557     ± 36.118  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6357.781     ± 31.961  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        902.338     ± 59.758  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        719.514     ± 68.470  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5728.290    ± 607.765  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12304.405     ± 33.148  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4474.656    ± 145.775  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3000.547    ± 235.074  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4498.968     ± 40.842  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23592.294    ± 531.796  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23171.494    ± 624.401  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474851.522   ± 2281.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481385.580   ± 2367.778  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494024.059   ± 3904.008  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502918.011   ± 3628.825  ops/s
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
