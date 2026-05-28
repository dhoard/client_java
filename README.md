# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-28T07:16:52Z
- **Commit:** [`ba6b0b5`](https://github.com/dhoard/client_java/commit/ba6b0b5a95b98ad40d2b513f3e446fdfbf94d0ab)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.33K | ± 512.56 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.19K | ± 435.16 | ops/s | 1.2x slower |
| prometheusAdd | 48.52K | ± 155.94 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.26K | ± 593.88 | ops/s | 1.3x slower |
| simpleclientInc | 6.17K | ± 43.14 | ops/s | 9.6x slower |
| simpleclientAdd | 5.97K | ± 148.52 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.92K | ± 21.98 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.89K | ± 40.22 | ops/s | 10x slower |
| openTelemetryInc | 3.78K | ± 219.18 | ops/s | 16x slower |
| openTelemetryAdd | 3.28K | ± 184.66 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.59K | ± 49.91 | ops/s | **fastest** |
| prometheusClassic | 4.39K | ± 604.60 | ops/s | 1.0x slower |
| prometheusNative | 2.98K | ± 274.98 | ops/s | 1.5x slower |
| openTelemetryClassic | 693.92 | ± 22.50 | ops/s | 6.6x slower |
| openTelemetryExponential | 525.90 | ± 18.20 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.27K | ± 171.69 | ops/s | **fastest** |
| prometheusWriteToNull | 27.17K | ± 197.56 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.35K | ± 6.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.10K | ± 2.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 547.81K | ± 9.04K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 536.31K | ± 2.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44261.450    ± 593.879  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3275.483    ± 184.657  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3779.172    ± 219.176  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5888.559     ± 40.220  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48520.128    ± 155.943  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59327.546    ± 512.565  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51187.616    ± 435.156  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5973.226    ± 148.516  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6165.660     ± 43.136  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5924.455     ± 21.981  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.916     ± 22.500  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        525.899     ± 18.202  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4392.376    ± 604.596  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2980.527    ± 274.983  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4587.865     ± 49.914  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27266.561    ± 171.691  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27165.023    ± 197.563  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536312.616   ± 2820.178  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     547808.674   ± 9036.407  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568099.389   ± 2704.660  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581350.150   ± 6732.514  ops/s
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
