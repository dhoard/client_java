# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-13T06:40:07Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.16K | ± 604.52 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.25K | ± 120.64 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 193.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.06K | ± 1.69K | ops/s | 1.4x slower |
| simpleclientInc | 6.52K | ± 183.08 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.43K | ± 139.20 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 326.02 | ops/s | 11x slower |
| openTelemetryInc | 3.35K | ± 262.47 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.26K | ± 226.64 | ops/s | 20x slower |
| openTelemetryAdd | 3.09K | ± 110.06 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 1.06K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 79.37 | ops/s | 1.1x slower |
| prometheusNative | 2.86K | ± 305.34 | ops/s | 1.8x slower |
| openTelemetryClassic | 746.85 | ± 34.06 | ops/s | 6.8x slower |
| openTelemetryExponential | 624.21 | ± 66.73 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.37K | ± 1.19K | ops/s | **fastest** |
| openMetricsWriteToNull | 24.03K | ± 830.71 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 508.50K | ± 8.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.96K | ± 5.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.67K | ± 9.02K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 470.13K | ± 6.96K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48063.189   ± 1693.039  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3086.809    ± 110.055  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3349.518    ± 262.467  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3260.374    ± 226.640  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51287.770    ± 193.167  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66159.986    ± 604.522  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56251.987    ± 120.638  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6080.425    ± 326.015  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6523.160    ± 183.079  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6431.340    ± 139.201  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        746.854     ± 34.059  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        624.206     ± 66.731  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5043.422   ± 1058.444  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2862.561    ± 305.335  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.261     ± 79.368  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24031.512    ± 830.714  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24373.069   ± 1193.832  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470125.908   ± 6959.028  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481672.748   ± 9021.559  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490963.044   ± 5629.739  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508496.114   ± 8943.823  ops/s
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
