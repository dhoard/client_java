# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-07T07:29:40Z
- **Commit:** [`574fb73`](https://github.com/dhoard/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.22K | ± 1.33K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.97K | ± 1.19K | ops/s | 1.2x slower |
| prometheusAdd | 51.63K | ± 89.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.80K | ± 7.81K | ops/s | 1.5x slower |
| simpleclientInc | 6.58K | ± 11.44 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.39K | ± 23.51 | ops/s | 10x slower |
| simpleclientAdd | 6.08K | ± 353.41 | ops/s | 11x slower |
| openTelemetryInc | 3.39K | ± 498.74 | ops/s | 19x slower |
| openTelemetryAdd | 3.23K | ± 104.92 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.17K | ± 163.56 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.24K | ± 2.11K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 48.03 | ops/s | 1.2x slower |
| prometheusNative | 2.97K | ± 343.48 | ops/s | 1.8x slower |
| openTelemetryClassic | 778.79 | ± 8.20 | ops/s | 6.7x slower |
| openTelemetryExponential | 644.29 | ± 71.17 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.39K | ± 124.92 | ops/s | **fastest** |
| prometheusWriteToNull | 22.86K | ± 186.03 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.39K | ± 4.52K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.36K | ± 4.63K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.45K | ± 5.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.51K | ± 13.26K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43799.655   ± 7807.966  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3228.365    ± 104.920  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3390.436    ± 498.740  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3169.372    ± 163.555  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51628.649     ± 89.785  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65224.426   ± 1328.887  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55973.541   ± 1187.230  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6081.102    ± 353.408  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6580.131     ± 11.435  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6387.032     ± 23.510  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        778.793      ± 8.198  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        644.291     ± 71.169  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5239.507   ± 2113.672  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2971.944    ± 343.479  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.165     ± 48.031  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23392.551    ± 124.917  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22863.886    ± 186.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476506.499  ± 13259.299  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488450.621   ± 5381.072  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505364.466   ± 4626.246  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512391.180   ± 4524.905  ops/s
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
