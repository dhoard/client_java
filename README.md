# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-25T05:42:41Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.86K | ± 52.41 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.51K | ± 1.26K | ops/s | 1.2x slower |
| prometheusAdd | 48.13K | ± 320.37 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.97K | ± 243.42 | ops/s | 1.4x slower |
| simpleclientInc | 6.26K | ± 132.73 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 5.95K | ± 235.13 | ops/s | 10x slower |
| simpleclientAdd | 5.92K | ± 373.61 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 148.76 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.39K | ± 57.04 | ops/s | 43x slower |
| openTelemetryInc | 1.31K | ± 148.23 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 1.39K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 116.45 | ops/s | 1.2x slower |
| prometheusNative | 3.02K | ± 219.20 | ops/s | 1.7x slower |
| openTelemetryClassic | 596.37 | ± 12.86 | ops/s | 8.8x slower |
| openTelemetryExponential | 504.09 | ± 16.04 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.34K | ± 4.09K | ops/s | **fastest** |
| prometheusWriteToByteArray | 541.37K | ± 12.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 536.13K | ± 3.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 517.69K | ± 11.97K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43970.446    ± 243.418  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1441.259    ± 148.758  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1309.181    ± 148.232  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1392.154     ± 57.042  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48133.563    ± 320.367  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59861.197     ± 52.407  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51508.839   ± 1259.486  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5917.797    ± 373.607  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6261.837    ± 132.729  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5948.609    ± 235.126  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        596.373     ± 12.858  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        504.088     ± 16.035  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5256.765   ± 1393.529  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3021.782    ± 219.198  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.833    ± 116.446  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     517690.204  ± 11967.443  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     536126.944   ± 3362.128  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541372.412  ± 12129.651  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555339.187   ± 4094.991  ops/s
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
