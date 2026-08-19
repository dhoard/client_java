# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-19T04:13:25Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.63K | ± 846.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.35K | ± 1.07K | ops/s | 1.2x slower |
| prometheusAdd | 51.39K | ± 143.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.42K | ± 856.50 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 18.53K | ± 24.48 | ops/s | 3.5x slower |
| openTelemetryInc | 15.20K | ± 146.76 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.82K | ± 241.53 | ops/s | 5.1x slower |
| simpleclientInc | 6.63K | ± 74.95 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.36K | ± 32.54 | ops/s | 10x slower |
| simpleclientAdd | 6.26K | ± 365.83 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.28K | ± 37.53 | ops/s | **fastest** |
| prometheusClassic | 5.49K | ± 1.73K | ops/s | 2.2x slower |
| prometheusClassicSingleThread | 4.57K | ± 25.00 | ops/s | 2.7x slower |
| simpleclient | 4.48K | ± 47.38 | ops/s | 2.7x slower |
| prometheusNative | 2.80K | ± 446.37 | ops/s | 4.4x slower |
| openTelemetryClassic | 900.70 | ± 73.37 | ops/s | 14x slower |
| openTelemetryExponential | 827.31 | ± 105.69 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.57K | ± 723.49 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.38K | ± 656.76 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 515.86K | ± 3.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 504.41K | ± 1.83K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 492.33K | ± 999.77 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.85K | ± 5.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47418.197    ± 856.496  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12817.441    ± 241.530  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15197.689    ± 146.758  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18527.616     ± 24.478  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51390.656    ± 143.267  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65625.443    ± 846.212  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56352.524   ± 1068.834  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6263.372    ± 365.827  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.289     ± 74.945  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6357.528     ± 32.543  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        900.702     ± 73.365  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        827.312    ± 105.692  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5490.723   ± 1730.930  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12282.691     ± 37.533  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4568.965     ± 24.999  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2802.632    ± 446.371  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4476.843     ± 47.380  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23377.227    ± 656.760  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23565.154    ± 723.488  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     492326.165    ± 999.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489854.932   ± 5532.675  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     504412.685   ± 1825.948  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515862.895   ± 3014.076  ops/s
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
