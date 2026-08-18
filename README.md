# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-18T04:11:37Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.04K | ± 206.34 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 495.90 | ops/s | 1.2x slower |
| prometheusAdd | 48.66K | ± 748.94 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.84K | ± 515.26 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 17.21K | ± 93.91 | ops/s | 3.5x slower |
| openTelemetryInc | 14.03K | ± 362.05 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.13K | ± 148.00 | ops/s | 4.9x slower |
| simpleclientAdd | 6.13K | ± 124.69 | ops/s | 9.8x slower |
| simpleclientInc | 6.13K | ± 49.98 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.83K | ± 107.33 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.63K | ± 108.84 | ops/s | **fastest** |
| prometheusClassic | 5.78K | ± 1.09K | ops/s | 2.4x slower |
| prometheusClassicSingleThread | 5.60K | ± 323.75 | ops/s | 2.4x slower |
| simpleclient | 4.46K | ± 124.28 | ops/s | 3.1x slower |
| prometheusNative | 2.96K | ± 182.46 | ops/s | 4.6x slower |
| openTelemetryClassic | 808.80 | ± 69.06 | ops/s | 17x slower |
| openTelemetryExponential | 717.50 | ± 40.29 | ops/s | 19x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.39K | ± 121.63 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.32K | ± 238.49 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 582.41K | ± 1.82K | ops/s | **fastest** |
| prometheusWriteToByteArray | 571.16K | ± 5.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.01K | ± 4.15K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 534.40K | ± 6.05K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43835.500    ± 515.257  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12130.977    ± 148.003  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14028.975    ± 362.055  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17206.581     ± 93.907  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48660.628    ± 748.939  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60038.920    ± 206.339  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51468.268    ± 495.897  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6130.870    ± 124.694  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6126.891     ± 49.983  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5833.082    ± 107.327  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        808.800     ± 69.059  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        717.500     ± 40.290  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5777.021   ± 1092.822  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13630.462    ± 108.845  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5602.438    ± 323.752  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.926    ± 182.455  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4460.058    ± 124.280  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27322.538    ± 238.490  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27393.383    ± 121.627  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     534398.782   ± 6053.451  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548011.776   ± 4149.439  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     571155.464   ± 5056.067  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582405.747   ± 1819.237  ops/s
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
