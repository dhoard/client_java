# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-24T07:14:38Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.61K | ± 420.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.22K | ± 2.54K | ops/s | 1.2x slower |
| prometheusAdd | 48.37K | ± 1.30K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.29K | ± 1.29K | ops/s | 1.4x slower |
| simpleclientInc | 6.10K | ± 83.31 | ops/s | 9.8x slower |
| simpleclientAdd | 6.09K | ± 30.84 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.02K | ± 168.99 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 5.45K | ± 828.00 | ops/s | 11x slower |
| openTelemetryInc | 4.48K | ± 958.08 | ops/s | 13x slower |
| openTelemetryAdd | 3.75K | ± 882.69 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.44K | ± 200.80 | ops/s | **fastest** |
| prometheusClassic | 4.43K | ± 804.13 | ops/s | 1.0x slower |
| prometheusNative | 3.14K | ± 112.38 | ops/s | 1.4x slower |
| openTelemetryClassic | 701.23 | ± 36.88 | ops/s | 6.3x slower |
| openTelemetryExponential | 538.36 | ± 37.02 | ops/s | 8.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.17K | ± 290.13 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.13K | ± 302.14 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 563.55K | ± 4.00K | ops/s | **fastest** |
| prometheusWriteToByteArray | 546.06K | ± 6.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.72K | ± 3.29K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 520.09K | ± 5.25K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43288.564   ± 1286.712  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3754.439    ± 882.691  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4476.134    ± 958.082  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5454.154    ± 828.001  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48371.034   ± 1298.530  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59611.414    ± 420.674  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50216.436   ± 2543.628  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6089.841     ± 30.839  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6101.045     ± 83.305  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6017.818    ± 168.987  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.235     ± 36.875  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        538.363     ± 37.017  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4428.766    ± 804.127  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3135.080    ± 112.382  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4436.334    ± 200.799  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27133.076    ± 302.145  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27167.875    ± 290.129  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     520086.104   ± 5245.900  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533723.277   ± 3291.067  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     546056.455   ± 6271.712  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     563545.972   ± 4004.581  ops/s
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
