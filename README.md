# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-05T06:18:18Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.80K | ± 651.99 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.59K | ± 1.13K | ops/s | 1.2x slower |
| prometheusAdd | 50.28K | ± 508.84 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.69K | ± 1.85K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 18.19K | ± 169.95 | ops/s | 3.6x slower |
| openTelemetryInc | 14.59K | ± 365.00 | ops/s | 4.5x slower |
| openTelemetryAdd | 12.49K | ± 160.18 | ops/s | 5.3x slower |
| simpleclientInc | 6.55K | ± 43.45 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.29K | ± 47.33 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 199.15 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.30K | ± 77.87 | ops/s | **fastest** |
| prometheusClassic | 5.21K | ± 1.40K | ops/s | 2.4x slower |
| prometheusClassicSingleThread | 4.57K | ± 32.99 | ops/s | 2.7x slower |
| simpleclient | 4.47K | ± 32.06 | ops/s | 2.8x slower |
| prometheusNative | 3.17K | ± 61.85 | ops/s | 3.9x slower |
| openTelemetryExponential | 734.57 | ± 208.51 | ops/s | 17x slower |
| openTelemetryClassic | 731.34 | ± 13.79 | ops/s | 17x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.27K | ± 116.30 | ops/s | **fastest** |
| prometheusWriteToNull | 22.80K | ± 1.10K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 471.78K | ± 5.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 462.59K | ± 17.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 445.76K | ± 8.47K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 437.15K | ± 9.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48685.408   ± 1845.152  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12490.338    ± 160.176  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14585.621    ± 365.002  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18186.146    ± 169.950  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50280.383    ± 508.844  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65804.252    ± 651.994  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55594.445   ± 1127.209  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.573    ± 199.147  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.393     ± 43.449  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6291.249     ± 47.332  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        731.340     ± 13.794  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        734.574    ± 208.509  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5208.387   ± 1396.357  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12303.143     ± 77.867  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4573.668     ± 32.994  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3168.106     ± 61.848  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.526     ± 32.056  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23270.847    ± 116.301  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22804.901   ± 1102.155  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     445762.130   ± 8474.282  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     437154.171   ± 9658.072  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     462590.827  ± 17876.195  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     471778.836   ± 5766.082  ops/s
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
