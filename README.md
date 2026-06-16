# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-16T08:29:46Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.09K | ± 675.81 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.15K | ± 1.12K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.14K | ± 1.63K | ops/s | 1.0x slower |
| prometheusAdd | 28.46K | ± 51.29 | ops/s | 1.1x slower |
| simpleclientInc | 6.92K | ± 27.49 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.61K | ± 53.89 | ops/s | 4.7x slower |
| simpleclientAdd | 6.51K | ± 184.35 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 2.73K | ± 220.96 | ops/s | 11x slower |
| openTelemetryAdd | 2.39K | ± 424.18 | ops/s | 13x slower |
| openTelemetryInc | 2.32K | ± 97.68 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 141.08 | ops/s | **fastest** |
| prometheusClassic | 2.84K | ± 134.33 | ops/s | 1.5x slower |
| prometheusNative | 2.51K | ± 312.88 | ops/s | 1.7x slower |
| openTelemetryClassic | 629.40 | ± 55.59 | ops/s | 6.9x slower |
| openTelemetryExponential | 445.29 | ± 14.51 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.25K | ± 156.50 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.21K | ± 186.48 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 323.60K | ± 1.97K | ops/s | **fastest** |
| prometheusWriteToByteArray | 317.01K | ± 3.65K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 298.68K | ± 2.86K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 296.90K | ± 1.84K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30143.339   ± 1625.097  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2394.794    ± 424.178  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2318.104     ± 97.682  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2729.796    ± 220.958  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28461.840     ± 51.290  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31087.966    ± 675.812  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30154.108   ± 1122.658  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6514.089    ± 184.348  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6917.738     ± 27.492  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6614.604     ± 53.888  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        629.402     ± 55.592  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        445.286     ± 14.511  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2843.163    ± 134.326  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2510.146    ± 312.879  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4365.638    ± 141.080  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18206.509    ± 186.475  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18249.956    ± 156.495  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     296900.027   ± 1843.609  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     298683.919   ± 2863.569  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     317006.553   ± 3652.224  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     323602.897   ± 1971.178  ops/s
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
