# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-15T05:52:11Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.89K | ± 1.46K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.62K | ± 339.94 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 84.37 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.14K | ± 772.86 | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 173.39 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.44K | ± 128.05 | ops/s | 9.9x slower |
| simpleclientAdd | 6.21K | ± 168.00 | ops/s | 10x slower |
| openTelemetryAdd | 1.27K | ± 33.96 | ops/s | 50x slower |
| openTelemetryInc | 1.25K | ± 19.62 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.21K | ± 4.52 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.30K | ± 303.65 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 24.08 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 245.39 | ops/s | 1.9x slower |
| openTelemetryClassic | 695.40 | ± 2.56 | ops/s | 7.6x slower |
| openTelemetryExponential | 546.90 | ± 9.27 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.34K | ± 4.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.96K | ± 6.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.31K | ± 3.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.41K | ± 2.40K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48136.909    ± 772.856  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1267.847     ± 33.960  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1254.469     ± 19.617  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1207.094      ± 4.518  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51301.970     ± 84.369  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63891.769   ± 1461.226  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56615.843    ± 339.938  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6208.470    ± 167.996  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6588.971    ± 173.390  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6443.485    ± 128.051  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.400      ± 2.558  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        546.901      ± 9.268  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5304.394    ± 303.651  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2785.488    ± 245.390  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4401.198     ± 24.080  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475411.386   ± 2401.349  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480312.689   ± 3633.345  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482956.761   ± 6361.183  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487337.891   ± 4908.032  ops/s
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
