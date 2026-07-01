# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-01T07:32:55Z
- **Commit:** [`2a2c73d`](https://github.com/dhoard/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.55K | ± 4.56K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.50K | ± 1.30K | ops/s | 1.1x slower |
| prometheusAdd | 51.25K | ± 542.23 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 49.20K | ± 1.53K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 14.47 | ops/s | 9.7x slower |
| simpleclientAdd | 6.44K | ± 13.89 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.30K | ± 58.21 | ops/s | 10x slower |
| openTelemetryAdd | 3.41K | ± 189.79 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.36K | ± 281.18 | ops/s | 19x slower |
| openTelemetryInc | 2.99K | ± 128.15 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.72K | ± 707.02 | ops/s | **fastest** |
| simpleclient | 4.27K | ± 206.98 | ops/s | 1.3x slower |
| prometheusNative | 3.21K | ± 86.18 | ops/s | 1.8x slower |
| openTelemetryClassic | 792.23 | ± 21.94 | ops/s | 7.2x slower |
| openTelemetryExponential | 690.64 | ± 125.21 | ops/s | 8.3x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.84K | ± 680.99 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.32K | ± 1.17K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.92K | ± 5.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 505.56K | ± 5.19K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.62K | ± 1.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.57K | ± 9.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49199.922   ± 1528.017  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3408.291    ± 189.787  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2990.682    ± 128.153  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3360.435    ± 281.185  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51248.931    ± 542.227  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63546.794   ± 4558.414  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55504.916   ± 1304.496  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6443.991     ± 13.887  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6570.865     ± 14.471  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6299.317     ± 58.207  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        792.230     ± 21.942  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        690.643    ± 125.209  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5717.255    ± 707.022  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3206.339     ± 86.181  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4267.947    ± 206.980  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23319.109   ± 1167.535  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23839.230    ± 680.988  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481566.435   ± 9544.828  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491618.063   ± 1228.492  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     505560.600   ± 5186.002  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511921.822   ± 5580.628  ops/s
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
