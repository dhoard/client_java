# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-04T05:13:44Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.39K | ± 325.14 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.70K | ± 230.00 | ops/s | 1.2x slower |
| prometheusAdd | 51.39K | ± 528.35 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.60K | ± 1.34K | ops/s | 1.4x slower |
| simpleclientInc | 6.72K | ± 52.60 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.40K | ± 184.47 | ops/s | 10x slower |
| simpleclientAdd | 6.04K | ± 105.85 | ops/s | 11x slower |
| openTelemetryAdd | 1.73K | ± 67.39 | ops/s | 38x slower |
| openTelemetryInc | 1.27K | ± 115.35 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.25K | ± 95.73 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.86K | ± 1.44K | ops/s | **fastest** |
| simpleclient | 4.48K | ± 33.27 | ops/s | 1.3x slower |
| prometheusNative | 3.02K | ± 263.66 | ops/s | 1.9x slower |
| openTelemetryClassic | 695.29 | ± 52.54 | ops/s | 8.4x slower |
| openTelemetryExponential | 587.13 | ± 30.76 | ops/s | 10.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.66K | ± 1.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 489.06K | ± 1.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.67K | ± 2.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 480.06K | ± 6.71K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48604.032   ± 1336.900  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1728.696     ± 67.390  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1270.619    ± 115.354  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1254.621     ± 95.732  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51390.203    ± 528.355  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66387.215    ± 325.140  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56700.668    ± 230.002  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6035.719    ± 105.847  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6719.122     ± 52.603  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6400.603    ± 184.466  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.287     ± 52.535  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        587.130     ± 30.762  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5856.164   ± 1439.664  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3015.466    ± 263.664  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4480.205     ± 33.271  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     480060.641   ± 6714.121  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487674.934   ± 2940.466  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489062.460   ± 1568.949  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493662.044   ± 1197.120  ops/s
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
