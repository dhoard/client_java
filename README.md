# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-13T05:22:59Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 57.37K | ± 3.60K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.67K | ± 813.03 | ops/s | 1.1x slower |
| prometheusAdd | 48.59K | ± 384.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.99K | ± 132.17 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 17.25K | ± 99.74 | ops/s | 3.3x slower |
| openTelemetryInc | 13.86K | ± 108.38 | ops/s | 4.1x slower |
| openTelemetryAdd | 12.18K | ± 44.10 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.16K | ± 178.95 | ops/s | 9.3x slower |
| simpleclientInc | 6.11K | ± 49.56 | ops/s | 9.4x slower |
| simpleclientAdd | 5.85K | ± 291.05 | ops/s | 9.8x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.94K | ± 53.84 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.82K | ± 16.73 | ops/s | 2.4x slower |
| prometheusClassic | 5.03K | ± 1.68K | ops/s | 2.8x slower |
| simpleclient | 4.50K | ± 60.41 | ops/s | 3.1x slower |
| prometheusNative | 2.92K | ± 259.98 | ops/s | 4.8x slower |
| openTelemetryClassic | 802.26 | ± 99.23 | ops/s | 17x slower |
| openTelemetryExponential | 712.51 | ± 19.61 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.41K | ± 383.75 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.40K | ± 128.07 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 577.61K | ± 5.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 564.87K | ± 9.42K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 549.92K | ± 2.55K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.63K | ± 5.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43988.634    ± 132.173  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12183.160     ± 44.096  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13857.466    ± 108.377  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17248.369     ± 99.744  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48587.296    ± 384.064  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57369.547   ± 3600.040  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51667.343    ± 813.026  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5853.697    ± 291.045  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6114.516     ± 49.561  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6162.305    ± 178.949  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        802.263     ± 99.226  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        712.513     ± 19.608  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5032.163   ± 1681.571  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13941.587     ± 53.840  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5817.609     ± 16.726  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2922.855    ± 259.981  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4504.160     ± 60.407  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27399.938    ± 128.070  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27407.422    ± 383.755  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532627.577   ± 5794.443  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     549917.117   ± 2551.210  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     564873.562   ± 9417.131  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     577613.988   ± 5188.365  ops/s
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
