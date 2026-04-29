# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-29T06:33:00Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.20K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 47.38K | ± 4.28K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.10K | ± 696.52 | ops/s | 1.4x slower |
| prometheusAdd | 43.94K | ± 6.60K | ops/s | 1.4x slower |
| simpleclientInc | 6.06K | ± 212.86 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.97K | ± 215.23 | ops/s | 10x slower |
| simpleclientAdd | 5.91K | ± 148.54 | ops/s | 10x slower |
| openTelemetryInc | 1.51K | ± 109.37 | ops/s | 40x slower |
| openTelemetryIncNoLabels | 1.44K | ± 40.26 | ops/s | 42x slower |
| openTelemetryAdd | 1.38K | ± 67.90 | ops/s | 43x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.26K | ± 1.77K | ops/s | **fastest** |
| simpleclient | 4.33K | ± 53.13 | ops/s | 1.4x slower |
| prometheusNative | 2.82K | ± 89.98 | ops/s | 2.2x slower |
| openTelemetryClassic | 632.96 | ± 23.56 | ops/s | 9.9x slower |
| openTelemetryExponential | 522.41 | ± 24.20 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 534.93K | ± 1.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 524.79K | ± 4.54K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 521.79K | ± 4.08K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 510.39K | ± 3.42K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44099.549    ± 696.518  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1384.758     ± 67.898  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1510.269    ± 109.367  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1440.097     ± 40.260  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      43943.949   ± 6602.444  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60202.387   ± 1154.533  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      47381.978   ± 4281.723  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5909.459    ± 148.540  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6061.260    ± 212.855  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5973.868    ± 215.230  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        632.961     ± 23.557  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        522.414     ± 24.204  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6255.128   ± 1765.216  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2823.996     ± 89.981  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4327.192     ± 53.126  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     510385.226   ± 3418.855  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     521792.894   ± 4076.827  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     524790.709   ± 4536.546  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     534932.773   ± 1738.597  ops/s
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
