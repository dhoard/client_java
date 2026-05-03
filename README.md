# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-03T06:36:09Z
- **Commit:** [`188e434`](https://github.com/dhoard/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.10K | ± 30.30 | ops/s | **fastest** |
| prometheusInc | 29.52K | ± 1.68K | ops/s | 1.1x slower |
| codahaleIncNoLabels | 28.75K | ± 1.86K | ops/s | 1.1x slower |
| prometheusAdd | 28.05K | ± 620.47 | ops/s | 1.1x slower |
| simpleclientInc | 6.82K | ± 171.66 | ops/s | 4.6x slower |
| simpleclientAdd | 6.55K | ± 269.64 | ops/s | 4.7x slower |
| simpleclientNoLabelsInc | 6.47K | ± 232.58 | ops/s | 4.8x slower |
| openTelemetryInc | 2.53K | ± 145.64 | ops/s | 12x slower |
| openTelemetryAdd | 2.47K | ± 35.64 | ops/s | 13x slower |
| openTelemetryIncNoLabels | 2.45K | ± 101.59 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 91.63 | ops/s | **fastest** |
| prometheusClassic | 2.91K | ± 283.48 | ops/s | 1.5x slower |
| prometheusNative | 1.91K | ± 84.25 | ops/s | 2.3x slower |
| openTelemetryClassic | 635.16 | ± 29.19 | ops/s | 7.0x slower |
| openTelemetryExponential | 457.07 | ± 10.96 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 319.35K | ± 1.78K | ops/s | **fastest** |
| prometheusWriteToByteArray | 316.60K | ± 733.25 | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.19K | ± 2.57K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 298.64K | ± 1.09K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28750.322   ± 1862.738  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2471.946     ± 35.645  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2532.577    ± 145.640  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2450.874    ± 101.593  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28048.674    ± 620.466  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29516.622   ± 1684.524  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31096.940     ± 30.305  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6548.407    ± 269.642  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6821.807    ± 171.661  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6467.738    ± 232.579  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        635.157     ± 29.191  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        457.072     ± 10.964  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2906.564    ± 283.484  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       1911.192     ± 84.250  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4464.699     ± 91.632  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298639.560   ± 1093.423  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299193.603   ± 2565.345  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     316604.384    ± 733.252  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319352.201   ± 1779.181  ops/s
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
