# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-06T05:15:23Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.42K | ± 1.35K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.56K | ± 2.51K | ops/s | 1.2x slower |
| prometheusAdd | 51.53K | ± 275.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 1.54K | ops/s | 1.3x slower |
| simpleclientInc | 6.75K | ± 65.53 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.44K | ± 193.09 | ops/s | 10x slower |
| simpleclientAdd | 6.38K | ± 151.82 | ops/s | 10x slower |
| openTelemetryInc | 1.54K | ± 287.29 | ops/s | 43x slower |
| openTelemetryAdd | 1.54K | ± 246.64 | ops/s | 43x slower |
| openTelemetryIncNoLabels | 1.22K | ± 36.06 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.26K | ± 1.75K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 33.55 | ops/s | 1.2x slower |
| prometheusNative | 3.00K | ± 238.69 | ops/s | 1.8x slower |
| openTelemetryClassic | 663.69 | ± 34.41 | ops/s | 7.9x slower |
| openTelemetryExponential | 546.15 | ± 3.61 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.53K | ± 2.04K | ops/s | **fastest** |
| openMetricsWriteToNull | 481.35K | ± 1.94K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 479.94K | ± 4.56K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.17K | ± 1.83K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48465.146   ± 1542.669  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1537.636    ± 246.639  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1538.057    ± 287.294  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1215.382     ± 36.065  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51525.848    ± 275.295  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65424.061   ± 1353.811  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55561.574   ± 2509.935  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6375.138    ± 151.816  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6745.118     ± 65.528  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6442.562    ± 193.088  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        663.692     ± 34.406  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.146      ± 3.611  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5264.198   ± 1747.078  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3000.370    ± 238.689  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4561.901     ± 33.554  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472173.047   ± 1832.910  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481353.288   ± 1937.212  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479935.693   ± 4560.409  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490526.021   ± 2035.963  ops/s
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
