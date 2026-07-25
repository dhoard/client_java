# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-25T06:19:23Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.08K | ± 2.34K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.17K | ± 944.36 | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 337.79 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.91K | ± 541.37 | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 15.79 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.28K | ± 139.16 | ops/s | 10x slower |
| simpleclientAdd | 6.09K | ± 26.40 | ops/s | 11x slower |
| openTelemetryAdd | 3.15K | ± 166.05 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.09K | ± 301.38 | ops/s | 21x slower |
| openTelemetryInc | 3.04K | ± 332.85 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.54K | ± 77.07 | ops/s | **fastest** |
| prometheusClassic | 5.01K | ± 1.13K | ops/s | 2.5x slower |
| prometheusClassicSingleThread | 4.58K | ± 31.09 | ops/s | 2.7x slower |
| simpleclient | 4.40K | ± 77.18 | ops/s | 2.9x slower |
| prometheusNative | 2.67K | ± 84.67 | ops/s | 4.7x slower |
| openTelemetryClassic | 749.54 | ± 29.55 | ops/s | 17x slower |
| openTelemetryExponential | 711.52 | ± 22.22 | ops/s | 18x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.82K | ± 649.64 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.51K | ± 831.11 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 500.04K | ± 5.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.74K | ± 6.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.67K | ± 4.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.63K | ± 5.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49906.733    ± 541.366  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3147.002    ± 166.046  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3037.907    ± 332.851  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3086.992    ± 301.379  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51358.699    ± 337.790  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65077.719   ± 2342.634  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56171.451    ± 944.362  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6094.678     ± 26.400  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6587.893     ± 15.787  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6283.339    ± 139.163  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        749.538     ± 29.549  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        711.517     ± 22.219  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5008.332   ± 1131.459  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12538.651     ± 77.069  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4579.394     ± 31.089  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2667.126     ± 84.669  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4396.129     ± 77.183  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23511.050    ± 831.110  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23819.141    ± 649.635  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475630.070   ± 5404.367  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476672.631   ± 4956.234  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489736.653   ± 6627.533  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     500043.525   ± 5355.483  ops/s
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
