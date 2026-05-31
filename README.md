# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-31T07:24:33Z
- **Commit:** [`f0a3b2e`](https://github.com/dhoard/client_java/commit/f0a3b2e46296428952756c95c9037982e7e9baa7)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.34K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 188.16 | ops/s | 1.1x slower |
| prometheusAdd | 51.24K | ± 140.06 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.99K | ± 1.01K | ops/s | 1.3x slower |
| simpleclientInc | 6.53K | ± 33.34 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.34K | ± 9.79 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 279.11 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.48K | ± 608.19 | ops/s | 18x slower |
| openTelemetryInc | 3.14K | ± 566.64 | ops/s | 20x slower |
| openTelemetryAdd | 3.14K | ± 99.46 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.35K | ± 1.54K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 26.84 | ops/s | 1.2x slower |
| prometheusNative | 2.77K | ± 271.91 | ops/s | 1.9x slower |
| openTelemetryClassic | 745.35 | ± 42.30 | ops/s | 7.2x slower |
| openTelemetryExponential | 625.96 | ± 83.69 | ops/s | 8.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.99K | ± 740.22 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.70K | ± 559.68 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 516.72K | ± 5.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 509.45K | ± 7.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.92K | ± 1.01K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 489.82K | ± 787.49 | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47993.505   ± 1014.997  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3138.789     ± 99.457  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3142.444    ± 566.642  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3481.773    ± 608.192  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51236.164    ± 140.055  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64335.147   ± 1235.282  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56779.421    ± 188.165  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6327.046    ± 279.112  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6534.540     ± 33.336  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6343.486      ± 9.791  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        745.354     ± 42.304  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        625.964     ± 83.694  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5347.284   ± 1537.553  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2769.867    ± 271.906  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4370.359     ± 26.844  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23702.481    ± 559.682  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23990.024    ± 740.221  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     489821.366    ± 787.492  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491922.611   ± 1013.210  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     509449.142   ± 7021.174  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     516721.908   ± 5978.532  ops/s
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
