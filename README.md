# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-05T05:17:38Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.50K | ± 1.16K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.17K | ± 410.32 | ops/s | 1.1x slower |
| prometheusAdd | 50.54K | ± 1.22K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.21K | ± 4.23K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.60K | ± 136.57 | ops/s | 9.8x slower |
| simpleclientInc | 6.53K | ± 234.77 | ops/s | 9.9x slower |
| simpleclientAdd | 6.30K | ± 185.67 | ops/s | 10x slower |
| openTelemetryAdd | 1.52K | ± 213.88 | ops/s | 42x slower |
| openTelemetryInc | 1.24K | ± 41.82 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.22K | ± 47.68 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.80K | ± 721.67 | ops/s | **fastest** |
| simpleclient | 4.56K | ± 52.81 | ops/s | 1.1x slower |
| prometheusNative | 2.83K | ± 298.44 | ops/s | 1.7x slower |
| openTelemetryClassic | 678.86 | ± 27.62 | ops/s | 7.1x slower |
| openTelemetryExponential | 548.27 | ± 20.32 | ops/s | 8.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.22K | ± 1.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.48K | ± 1.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.77K | ± 3.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.64K | ± 4.65K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46210.347   ± 4233.082  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1519.680    ± 213.877  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1242.417     ± 41.821  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1221.367     ± 47.682  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50540.834   ± 1216.770  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64496.510   ± 1155.193  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57171.561    ± 410.322  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6303.896    ± 185.670  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.726    ± 234.769  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6603.503    ± 136.575  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        678.861     ± 27.625  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        548.269     ± 20.319  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4796.626    ± 721.670  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2831.703    ± 298.444  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4555.338     ± 52.812  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481766.178   ± 3271.726  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481641.122   ± 4651.773  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488481.470   ± 1886.958  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492224.033   ± 1811.879  ops/s
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
