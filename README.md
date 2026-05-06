# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-06T06:33:59Z
- **Commit:** [`0d33b2a`](https://github.com/dhoard/client_java/commit/0d33b2a21208a58f0c67c0e9a9b662044ded45d2)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.43K | ± 648.49 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.14K | ± 194.64 | ops/s | 1.2x slower |
| prometheusAdd | 51.10K | ± 693.24 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.14K | ± 1.25K | ops/s | 1.4x slower |
| simpleclientInc | 6.50K | ± 90.17 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 236.80 | ops/s | 11x slower |
| simpleclientAdd | 6.24K | ± 325.85 | ops/s | 11x slower |
| openTelemetryInc | 3.42K | ± 276.50 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.18K | ± 89.12 | ops/s | 21x slower |
| openTelemetryAdd | 3.14K | ± 121.91 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.76K | ± 792.14 | ops/s | **fastest** |
| simpleclient | 4.47K | ± 36.39 | ops/s | 1.1x slower |
| prometheusNative | 2.95K | ± 372.31 | ops/s | 1.6x slower |
| openTelemetryClassic | 771.92 | ± 22.54 | ops/s | 6.2x slower |
| openTelemetryExponential | 681.13 | ± 46.03 | ops/s | 7.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.49K | ± 3.21K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.90K | ± 6.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.39K | ± 2.38K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.86K | ± 2.67K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49136.669   ± 1249.885  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3136.529    ± 121.909  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3421.062    ± 276.498  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3178.632     ± 89.120  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51102.593    ± 693.245  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66431.579    ± 648.495  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57142.068    ± 194.643  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6237.720    ± 325.848  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6497.019     ± 90.171  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6325.812    ± 236.798  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        771.915     ± 22.537  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        681.132     ± 46.032  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4756.630    ± 792.137  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2951.998    ± 372.310  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4471.922     ± 36.392  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470857.119   ± 2669.994  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480386.648   ± 2382.526  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482899.480   ± 6433.427  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490485.449   ± 3207.298  ops/s
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
