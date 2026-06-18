# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-18T07:59:31Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.35K | ± 2.28K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.19K | ± 141.08 | ops/s | 1.1x slower |
| prometheusAdd | 50.41K | ± 2.12K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.96K | ± 541.67 | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 5.93 | ops/s | 9.8x slower |
| simpleclientAdd | 6.48K | ± 57.14 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.39K | ± 32.82 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.02K | ± 64.18 | ops/s | 21x slower |
| openTelemetryAdd | 2.97K | ± 27.28 | ops/s | 22x slower |
| openTelemetryInc | 2.97K | ± 71.55 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.18K | ± 2.28K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 66.95 | ops/s | 1.2x slower |
| prometheusNative | 2.80K | ± 257.98 | ops/s | 1.9x slower |
| openTelemetryClassic | 769.24 | ± 12.06 | ops/s | 6.7x slower |
| openTelemetryExponential | 650.70 | ± 60.96 | ops/s | 8.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.62K | ± 598.31 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.59K | ± 990.11 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.47K | ± 5.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.19K | ± 5.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.11K | ± 2.17K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.52K | ± 7.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49962.621    ± 541.670  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2972.450     ± 27.283  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2969.012     ± 71.552  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3021.904     ± 64.180  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50412.634   ± 2122.374  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64352.513   ± 2280.802  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57193.217    ± 141.081  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6482.893     ± 57.141  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6590.827      ± 5.928  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6386.835     ± 32.816  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        769.239     ± 12.055  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        650.697     ± 60.956  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5181.991   ± 2283.254  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2797.202    ± 257.984  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4436.763     ± 66.948  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23585.219    ± 990.113  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23619.450    ± 598.312  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479516.071   ± 7481.507  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488106.524   ± 2174.042  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503186.773   ± 5962.126  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504465.991   ± 5451.370  ops/s
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
