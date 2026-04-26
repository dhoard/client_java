# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-26T06:06:06Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.14K | ± 1.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 467.63 | ops/s | 1.1x slower |
| prometheusAdd | 51.60K | ± 177.06 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.53K | ± 2.24K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.51K | ± 138.44 | ops/s | 9.9x slower |
| simpleclientInc | 6.45K | ± 167.53 | ops/s | 9.9x slower |
| simpleclientAdd | 6.30K | ± 243.94 | ops/s | 10x slower |
| openTelemetryInc | 1.27K | ± 103.15 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.22K | ± 114.14 | ops/s | 53x slower |
| openTelemetryAdd | 1.21K | ± 22.12 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 980.94 | ops/s | **fastest** |
| simpleclient | 4.45K | ± 57.57 | ops/s | 1.2x slower |
| prometheusNative | 2.91K | ± 175.08 | ops/s | 1.8x slower |
| openTelemetryClassic | 685.50 | ± 20.54 | ops/s | 7.7x slower |
| openTelemetryExponential | 546.03 | ± 24.25 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.21K | ± 2.85K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.32K | ± 5.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.82K | ± 1.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.26K | ± 5.25K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48526.761   ± 2238.317  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1210.144     ± 22.115  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1273.627    ± 103.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1219.907    ± 114.140  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51598.688    ± 177.058  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64141.915   ± 1146.173  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56875.842    ± 467.631  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6303.621    ± 243.939  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6448.075    ± 167.528  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6506.320    ± 138.439  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.504     ± 20.541  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.033     ± 24.250  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5255.109    ± 980.935  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2910.410    ± 175.080  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4453.961     ± 57.575  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474257.635   ± 5254.137  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483822.186   ± 1609.962  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484316.888   ± 5598.084  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488210.755   ± 2847.019  ops/s
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
