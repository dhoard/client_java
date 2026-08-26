# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-26T04:21:11Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.30K | ± 450.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.05K | ± 416.39 | ops/s | 1.1x slower |
| prometheusAdd | 48.20K | ± 399.41 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.54K | ± 624.81 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 15.84K | ± 2.14K | ops/s | 3.7x slower |
| openTelemetryInc | 13.89K | ± 63.07 | ops/s | 4.3x slower |
| openTelemetryAdd | 11.95K | ± 306.25 | ops/s | 5.0x slower |
| simpleclientInc | 6.12K | ± 72.51 | ops/s | 9.7x slower |
| simpleclientAdd | 5.98K | ± 280.48 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.91K | ± 24.15 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.77K | ± 184.42 | ops/s | **fastest** |
| prometheusClassic | 6.55K | ± 1.27K | ops/s | 2.1x slower |
| prometheusClassicSingleThread | 5.82K | ± 11.19 | ops/s | 2.4x slower |
| simpleclient | 4.47K | ± 72.15 | ops/s | 3.1x slower |
| prometheusNative | 2.81K | ± 208.03 | ops/s | 4.9x slower |
| openTelemetryClassic | 803.05 | ± 13.45 | ops/s | 17x slower |
| openTelemetryExponential | 704.02 | ± 48.85 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.56K | ± 69.70 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.26K | ± 384.09 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 579.72K | ± 4.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 567.87K | ± 4.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.03K | ± 2.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 534.09K | ± 3.34K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43542.598    ± 624.814  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11947.635    ± 306.254  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13886.564     ± 63.070  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      15839.433   ± 2136.480  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48200.219    ± 399.405  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59301.102    ± 450.732  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52052.901    ± 416.394  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5978.934    ± 280.480  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6121.275     ± 72.508  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5906.990     ± 24.152  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        803.048     ± 13.449  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        704.016     ± 48.854  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6547.105   ± 1270.525  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13774.484    ± 184.424  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5820.008     ± 11.191  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2812.883    ± 208.032  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4474.636     ± 72.152  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27264.498    ± 384.087  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27562.373     ± 69.705  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     534092.451   ± 3339.078  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548027.622   ± 2631.324  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     567866.804   ± 4361.770  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579718.655   ± 4896.826  ops/s
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
