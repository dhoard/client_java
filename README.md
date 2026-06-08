# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-08T07:44:35Z
- **Commit:** [`574fb73`](https://github.com/dhoard/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.05K | ± 1.25K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.51K | ± 719.35 | ops/s | 1.2x slower |
| prometheusAdd | 51.56K | ± 92.17 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.75K | ± 1.57K | ops/s | 1.4x slower |
| simpleclientInc | 6.55K | ± 46.07 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.34K | ± 12.35 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 175.50 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.33K | ± 497.26 | ops/s | 20x slower |
| openTelemetryAdd | 3.31K | ± 305.00 | ops/s | 20x slower |
| openTelemetryInc | 3.22K | ± 287.62 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.65K | ± 425.64 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 72.45 | ops/s | 1.0x slower |
| prometheusNative | 2.98K | ± 412.97 | ops/s | 1.6x slower |
| openTelemetryClassic | 774.48 | ± 30.21 | ops/s | 6.0x slower |
| openTelemetryExponential | 644.61 | ± 38.49 | ops/s | 7.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.60K | ± 705.35 | ops/s | **fastest** |
| prometheusWriteToNull | 22.97K | ± 877.60 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 496.64K | ± 4.07K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.48K | ± 2.00K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.32K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.47K | ± 7.75K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47753.853   ± 1565.724  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3306.892    ± 304.996  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3215.465    ± 287.617  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3329.263    ± 497.263  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51560.283     ± 92.168  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65049.480   ± 1251.836  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56506.070    ± 719.348  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6308.565    ± 175.504  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6552.461     ± 46.068  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6341.780     ± 12.354  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        774.476     ± 30.208  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        644.612     ± 38.493  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4653.168    ± 425.644  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2983.402    ± 412.968  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.053     ± 72.453  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23600.869    ± 705.352  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22966.310    ± 877.601  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468465.296   ± 7749.808  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475322.288   ± 3501.132  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493481.350   ± 2004.208  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496644.796   ± 4065.948  ops/s
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
