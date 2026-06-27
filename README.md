# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-27T07:02:04Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.52K | ± 469.78 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.17K | ± 450.70 | ops/s | 1.2x slower |
| prometheusAdd | 48.06K | ± 486.68 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.02K | ± 313.16 | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 18.35 | ops/s | 9.6x slower |
| simpleclientAdd | 6.12K | ± 35.35 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.86K | ± 76.28 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.61K | ± 994.03 | ops/s | 13x slower |
| openTelemetryAdd | 4.32K | ± 944.65 | ops/s | 14x slower |
| openTelemetryInc | 3.97K | ± 210.44 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.19K | ± 875.83 | ops/s | **fastest** |
| simpleclient | 4.35K | ± 152.27 | ops/s | 1.4x slower |
| prometheusNative | 3.04K | ± 169.84 | ops/s | 2.0x slower |
| openTelemetryClassic | 700.62 | ± 15.05 | ops/s | 8.8x slower |
| openTelemetryExponential | 557.78 | ± 4.31 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.59K | ± 138.97 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.23K | ± 156.43 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.41K | ± 11.17K | ops/s | **fastest** |
| prometheusWriteToByteArray | 554.29K | ± 7.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.32K | ± 2.65K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.16K | ± 4.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44021.223    ± 313.156  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4319.423    ± 944.654  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3974.742    ± 210.442  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4612.392    ± 994.025  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48061.238    ± 486.677  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59522.497    ± 469.780  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51168.403    ± 450.697  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6115.516     ± 35.352  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6191.241     ± 18.349  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5864.222     ± 76.281  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.623     ± 15.049  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        557.777      ± 4.314  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6187.899    ± 875.826  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3044.560    ± 169.845  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4349.177    ± 152.275  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27229.851    ± 156.429  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27585.255    ± 138.969  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519157.107   ± 4862.911  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531316.577   ± 2650.110  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     554287.731   ± 7729.240  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555412.307  ± 11168.490  ops/s
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
