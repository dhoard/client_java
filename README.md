# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-13T07:23:58Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.77K | ± 1.22K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.60K | ± 1.15K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.90K | ± 931.31 | ops/s | 1.0x slower |
| prometheusAdd | 28.49K | ± 17.04 | ops/s | 1.1x slower |
| simpleclientInc | 6.67K | ± 58.54 | ops/s | 4.6x slower |
| simpleclientAdd | 6.54K | ± 248.00 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.49K | ± 260.54 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 2.60K | ± 220.00 | ops/s | 12x slower |
| openTelemetryInc | 2.58K | ± 78.24 | ops/s | 12x slower |
| openTelemetryAdd | 2.40K | ± 293.71 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.43K | ± 79.46 | ops/s | **fastest** |
| prometheusClassic | 3.33K | ± 349.36 | ops/s | 1.3x slower |
| prometheusNative | 2.31K | ± 145.58 | ops/s | 1.9x slower |
| openTelemetryClassic | 626.65 | ± 29.06 | ops/s | 7.1x slower |
| openTelemetryExponential | 443.65 | ± 26.63 | ops/s | 10.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 18.34K | ± 93.55 | ops/s | **fastest** |
| prometheusWriteToNull | 18.31K | ± 68.71 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 325.55K | ± 1.28K | ops/s | **fastest** |
| prometheusWriteToByteArray | 322.89K | ± 1.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 301.67K | ± 2.03K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 300.06K | ± 1.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29896.106    ± 931.312  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2399.982    ± 293.711  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2578.575     ± 78.244  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2600.163    ± 219.999  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28492.966     ± 17.037  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30768.003   ± 1223.165  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30602.308   ± 1150.680  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6535.436    ± 247.999  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6667.641     ± 58.541  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6494.693    ± 260.539  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        626.653     ± 29.060  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        443.649     ± 26.635  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3334.847    ± 349.356  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2313.948    ± 145.584  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4431.639     ± 79.462  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18343.054     ± 93.549  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18309.866     ± 68.709  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     300060.867   ± 1200.574  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     301673.425   ± 2033.198  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     322894.306   ± 1746.191  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     325553.698   ± 1276.601  ops/s
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
