# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-07T05:42:51Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.78K | ± 619.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 469.26 | ops/s | 1.2x slower |
| prometheusAdd | 48.44K | ± 47.48 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.07K | ± 149.76 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 16.48K | ± 1.15K | ops/s | 3.7x slower |
| openTelemetryInc | 13.85K | ± 61.63 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.01K | ± 198.76 | ops/s | 5.1x slower |
| simpleclientInc | 6.20K | ± 15.56 | ops/s | 9.8x slower |
| simpleclientAdd | 5.95K | ± 287.44 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.90K | ± 34.98 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.91K | ± 76.18 | ops/s | **fastest** |
| prometheusClassic | 6.77K | ± 1.77K | ops/s | 2.1x slower |
| prometheusClassicSingleThread | 5.77K | ± 204.33 | ops/s | 2.4x slower |
| simpleclient | 4.52K | ± 104.34 | ops/s | 3.1x slower |
| prometheusNative | 2.99K | ± 315.98 | ops/s | 4.7x slower |
| openTelemetryClassic | 805.33 | ± 46.38 | ops/s | 17x slower |
| openTelemetryExponential | 626.67 | ± 35.85 | ops/s | 22x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.41K | ± 341.64 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.36K | ± 164.16 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToByteArray | 568.13K | ± 4.97K | ops/s | **fastest** |
| prometheusWriteToNull | 562.34K | ± 8.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 541.34K | ± 5.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.09K | ± 3.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44072.726    ± 149.758  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12011.064    ± 198.756  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13851.272     ± 61.630  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16480.677   ± 1151.216  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48438.100     ± 47.483  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60782.710    ± 619.049  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51191.306    ± 469.259  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5954.474    ± 287.437  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6199.017     ± 15.561  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5901.117     ± 34.979  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        805.335     ± 46.377  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        626.669     ± 35.845  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6774.865   ± 1766.582  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13913.156     ± 76.177  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5768.992    ± 204.332  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2990.353    ± 315.979  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4522.198    ± 104.338  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27356.794    ± 164.160  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27414.743    ± 341.643  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527087.666   ± 3296.729  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     541338.203   ± 5344.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568134.608   ± 4969.800  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     562344.772   ± 8801.366  ops/s
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
