# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-19T05:57:45Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.55K | ± 1.58K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.22K | ± 219.53 | ops/s | 1.1x slower |
| prometheusAdd | 51.12K | ± 360.26 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.16K | ± 1.60K | ops/s | 1.4x slower |
| simpleclientInc | 6.49K | ± 321.68 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 170.94 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 205.03 | ops/s | 11x slower |
| openTelemetryInc | 1.49K | ± 193.64 | ops/s | 44x slower |
| openTelemetryAdd | 1.25K | ± 30.36 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.16K | ± 94.62 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.72K | ± 2.00K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 9.62 | ops/s | 1.3x slower |
| prometheusNative | 2.99K | ± 315.48 | ops/s | 1.9x slower |
| openTelemetryClassic | 671.71 | ± 20.43 | ops/s | 8.5x slower |
| openTelemetryExponential | 548.01 | ± 29.48 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.76K | ± 3.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.22K | ± 4.96K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.01K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.78K | ± 15.36K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48164.314   ± 1600.313  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1251.918     ± 30.356  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1487.860    ± 193.638  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1157.637     ± 94.616  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51119.695    ± 360.255  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65549.775   ± 1581.704  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57216.847    ± 219.528  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6191.584    ± 205.028  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6490.636    ± 321.683  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.708    ± 170.939  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        671.711     ± 20.434  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.013     ± 29.481  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5724.131   ± 1998.042  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2987.766    ± 315.478  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4395.422      ± 9.615  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473784.235  ± 15358.271  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488007.141   ± 3502.640  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491220.188   ± 4963.591  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493764.081   ± 3498.761  ops/s
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
