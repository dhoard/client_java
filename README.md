# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-10T05:07:32Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| codahaleIncNoLabels | 26.92K | ± 945.41 | ops/s | **fastest** |
| prometheusInc | 26.55K | ± 36.22 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 26.52K | ± 147.35 | ops/s | 1.0x slower |
| prometheusAdd | 25.82K | ± 579.34 | ops/s | 1.0x slower |
| openTelemetryIncNoLabels | 17.00K | ± 134.88 | ops/s | 1.6x slower |
| openTelemetryInc | 15.19K | ± 216.41 | ops/s | 1.8x slower |
| openTelemetryAdd | 13.19K | ± 142.83 | ops/s | 2.0x slower |
| simpleclientInc | 6.73K | ± 61.67 | ops/s | 4.0x slower |
| simpleclientNoLabelsInc | 6.61K | ± 31.22 | ops/s | 4.1x slower |
| simpleclientAdd | 6.57K | ± 26.69 | ops/s | 4.1x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 6.81K | ± 30.42 | ops/s | **fastest** |
| simpleclient | 4.31K | ± 13.15 | ops/s | 1.6x slower |
| prometheusClassicSingleThread | 2.91K | ± 81.96 | ops/s | 2.3x slower |
| prometheusClassic | 2.45K | ± 280.40 | ops/s | 2.8x slower |
| prometheusNative | 1.72K | ± 211.79 | ops/s | 4.0x slower |
| openTelemetryClassic | 439.98 | ± 66.83 | ops/s | 15x slower |
| openTelemetryExponential | 423.41 | ± 39.85 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 17.91K | ± 64.21 | ops/s | **fastest** |
| prometheusWriteToNull | 17.88K | ± 66.05 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 300.08K | ± 722.82 | ops/s | **fastest** |
| prometheusWriteToByteArray | 295.56K | ± 1.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 279.41K | ± 1.13K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 278.53K | ± 595.72 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26920.601    ± 945.407  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13189.632    ± 142.826  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15190.672    ± 216.406  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16996.274    ± 134.879  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25817.464    ± 579.343  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26550.428     ± 36.216  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26520.358    ± 147.350  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6565.841     ± 26.692  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6732.966     ± 61.670  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6612.474     ± 31.216  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        439.980     ± 66.828  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        423.407     ± 39.854  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2447.868    ± 280.400  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6809.904     ± 30.423  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2908.068     ± 81.962  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1721.666    ± 211.789  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4311.364     ± 13.155  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17909.153     ± 64.215  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17880.557     ± 66.049  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     278527.454    ± 595.725  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     279413.599   ± 1127.398  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     295556.837   ± 1662.218  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     300075.746    ± 722.821  ops/s
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
