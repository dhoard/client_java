# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-23T05:32:06Z
- **Commit:** [`ce5867b`](https://github.com/dhoard/client_java/commit/ce5867b3e25e10c68a6face275732b994a80ec98)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 30.80K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.46K | ± 1.01K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.24K | ± 229.63 | ops/s | 1.1x slower |
| prometheusAdd | 28.51K | ± 250.76 | ops/s | 1.1x slower |
| simpleclientInc | 7.11K | ± 50.87 | ops/s | 4.3x slower |
| simpleclientNoLabelsInc | 6.83K | ± 61.54 | ops/s | 4.5x slower |
| simpleclientAdd | 6.53K | ± 262.22 | ops/s | 4.7x slower |
| openTelemetryIncNoLabels | 1.49K | ± 80.54 | ops/s | 21x slower |
| openTelemetryInc | 1.39K | ± 28.61 | ops/s | 22x slower |
| openTelemetryAdd | 1.30K | ± 44.00 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.55K | ± 24.31 | ops/s | **fastest** |
| prometheusClassic | 4.25K | ± 1.77K | ops/s | 1.1x slower |
| prometheusNative | 2.21K | ± 53.09 | ops/s | 2.1x slower |
| openTelemetryClassic | 530.30 | ± 14.33 | ops/s | 8.6x slower |
| openTelemetryExponential | 417.91 | ± 5.04 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 262.63K | ± 624.07 | ops/s | **fastest** |
| prometheusWriteToByteArray | 260.66K | ± 947.75 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 249.05K | ± 611.36 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 248.80K | ± 1.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29242.884    ± 229.633  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1295.082     ± 44.004  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1389.328     ± 28.607  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1489.115     ± 80.539  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28512.476    ± 250.761  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30798.154   ± 1263.263  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30458.244   ± 1007.984  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6532.915    ± 262.220  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7114.620     ± 50.866  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6832.947     ± 61.537  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        530.298     ± 14.328  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        417.914      ± 5.040  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4254.664   ± 1771.947  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2210.838     ± 53.087  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4553.528     ± 24.311  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     248800.311   ± 1208.011  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     249047.080    ± 611.363  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     260659.501    ± 947.749  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     262628.759    ± 624.070  ops/s
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
