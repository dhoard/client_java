# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-14T05:55:33Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.39K | ± 6.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.47K | ± 910.19 | ops/s | 1.1x slower |
| prometheusAdd | 48.90K | ± 1.32K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.75K | ± 354.46 | ops/s | 1.3x slower |
| simpleclientInc | 6.16K | ± 62.47 | ops/s | 9.2x slower |
| simpleclientAdd | 5.90K | ± 356.11 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.88K | ± 71.86 | ops/s | 9.6x slower |
| openTelemetryInc | 5.27K | ± 1.53K | ops/s | 11x slower |
| openTelemetryAdd | 4.13K | ± 853.30 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.84K | ± 186.98 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 59.79 | ops/s | 1.2x slower |
| prometheusNative | 3.03K | ± 232.12 | ops/s | 1.8x slower |
| openTelemetryClassic | 744.72 | ± 28.20 | ops/s | 7.3x slower |
| openTelemetryExponential | 567.02 | ± 42.16 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.54K | ± 180.78 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.46K | ± 242.41 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 565.21K | ± 7.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 551.17K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.64K | ± 3.87K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 515.94K | ± 5.76K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43753.840    ± 354.463  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4128.855    ± 853.301  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5270.048   ± 1530.504  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3842.489    ± 186.975  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48902.458   ± 1317.945  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56392.182   ± 6826.626  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51470.322    ± 910.191  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5895.612    ± 356.108  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6162.685     ± 62.473  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5875.303     ± 71.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        744.719     ± 28.203  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.020     ± 42.159  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5420.282   ± 1630.094  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3031.076    ± 232.119  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4559.237     ± 59.790  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27456.373    ± 242.411  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27539.721    ± 180.781  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     515936.798   ± 5762.907  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533637.184   ± 3865.507  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     551165.602   ± 4112.832  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565208.395   ± 7969.903  ops/s
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
