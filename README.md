# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-24T07:10:11Z
- **Commit:** [`5ee188f`](https://github.com/dhoard/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.92K | ± 1.73K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 402.43 | ops/s | 1.1x slower |
| prometheusAdd | 48.32K | ± 331.98 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.37K | ± 666.68 | ops/s | 1.3x slower |
| simpleclientInc | 6.13K | ± 60.77 | ops/s | 9.4x slower |
| simpleclientNoLabelsInc | 5.89K | ± 10.73 | ops/s | 9.8x slower |
| simpleclientAdd | 5.88K | ± 201.60 | ops/s | 9.8x slower |
| openTelemetryInc | 4.34K | ± 1.23K | ops/s | 13x slower |
| openTelemetryIncNoLabels | 4.08K | ± 546.11 | ops/s | 14x slower |
| openTelemetryAdd | 3.74K | ± 991.76 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.90K | ± 1.64K | ops/s | **fastest** |
| simpleclient | 4.39K | ± 94.75 | ops/s | 1.3x slower |
| prometheusNative | 2.80K | ± 300.08 | ops/s | 2.1x slower |
| openTelemetryClassic | 691.68 | ± 12.80 | ops/s | 8.5x slower |
| openTelemetryExponential | 537.52 | ± 13.25 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.80K | ± 84.01 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.45K | ± 193.92 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.83K | ± 2.80K | ops/s | **fastest** |
| prometheusWriteToByteArray | 566.78K | ± 8.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.58K | ± 5.41K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.87K | ± 14.02K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44371.533    ± 666.677  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3737.593    ± 991.757  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4343.973   ± 1234.386  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4079.598    ± 546.110  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48315.932    ± 331.978  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57924.817   ± 1729.447  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51187.897    ± 402.426  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5881.241    ± 201.600  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6132.741     ± 60.769  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5894.929     ± 10.729  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        691.680     ± 12.800  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.520     ± 13.252  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5901.580   ± 1638.864  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2803.589    ± 300.082  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4393.894     ± 94.749  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27450.900    ± 193.924  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27796.932     ± 84.009  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532871.887  ± 14022.963  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543575.963   ± 5411.706  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     566779.060   ± 8499.919  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581831.852   ± 2795.228  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
