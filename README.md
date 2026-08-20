# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-20T04:13:01Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 63.61K | ± 1.97K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.37K | ± 134.34 | ops/s | 1.1x slower |
| prometheusAdd | 51.45K | ± 162.27 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.84K | ± 1.46K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.41K | ± 111.41 | ops/s | 3.5x slower |
| openTelemetryInc | 14.64K | ± 82.96 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.91K | ± 170.97 | ops/s | 4.9x slower |
| simpleclientInc | 6.56K | ± 34.57 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.34K | ± 14.09 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 188.67 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.23K | ± 131.58 | ops/s | **fastest** |
| prometheusClassicSingleThread | 4.56K | ± 37.26 | ops/s | 2.7x slower |
| simpleclient | 4.47K | ± 86.79 | ops/s | 2.7x slower |
| prometheusClassic | 4.24K | ± 857.03 | ops/s | 2.9x slower |
| prometheusNative | 2.57K | ± 137.79 | ops/s | 4.8x slower |
| openTelemetryExponential | 865.18 | ± 97.40 | ops/s | 14x slower |
| openTelemetryClassic | 780.06 | ± 44.16 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.99K | ± 560.94 | ops/s | **fastest** |
| prometheusWriteToNull | 23.58K | ± 1.15K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 508.77K | ± 4.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.93K | ± 5.08K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.42K | ± 3.39K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.77K | ± 4.33K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48839.374   ± 1457.596  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12913.036    ± 170.966  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14643.633     ± 82.959  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18408.075    ± 111.405  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51447.975    ± 162.274  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63607.128   ± 1973.588  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56371.638    ± 134.344  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6338.556    ± 188.673  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6555.443     ± 34.575  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6342.346     ± 14.088  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.061     ± 44.158  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        865.184     ± 97.396  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4242.585    ± 857.031  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12228.769    ± 131.581  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4555.309     ± 37.262  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2571.948    ± 137.793  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4466.167     ± 86.786  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23989.449    ± 560.945  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23578.426   ± 1153.688  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483767.870   ± 4331.382  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487424.031   ± 3386.714  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497926.018   ± 5082.505  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508772.403   ± 4822.486  ops/s
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
