# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-24T05:23:20Z
- **Commit:** [`ce5867b`](https://github.com/dhoard/client_java/commit/ce5867b3e25e10c68a6face275732b994a80ec98)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 315.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 779.03 | ops/s | 1.2x slower |
| prometheusAdd | 51.64K | ± 91.82 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.91K | ± 514.13 | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 40.84 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.69K | ± 30.11 | ops/s | 9.9x slower |
| simpleclientAdd | 6.12K | ± 69.17 | ops/s | 11x slower |
| openTelemetryAdd | 1.31K | ± 37.80 | ops/s | 51x slower |
| openTelemetryInc | 1.26K | ± 7.74 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.20K | ± 66.82 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.42K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 29.61 | ops/s | 1.2x slower |
| prometheusNative | 2.81K | ± 264.27 | ops/s | 1.9x slower |
| openTelemetryClassic | 718.37 | ± 23.05 | ops/s | 7.6x slower |
| openTelemetryExponential | 569.22 | ± 21.30 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 482.45K | ± 6.26K | ops/s | **fastest** |
| prometheusWriteToByteArray | 468.56K | ± 10.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 467.72K | ± 7.02K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 456.27K | ± 11.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49911.471    ± 514.129  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1307.598     ± 37.802  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1260.556      ± 7.737  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1196.226     ± 66.824  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51637.513     ± 91.819  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66070.550    ± 315.765  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56875.356    ± 779.030  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6118.930     ± 69.172  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6770.193     ± 40.844  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6692.415     ± 30.107  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        718.368     ± 23.054  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.223     ± 21.300  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5424.178   ± 1409.718  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2806.401    ± 264.274  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4544.357     ± 29.611  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     456271.544  ± 11544.750  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     467718.881   ± 7020.995  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     468562.712  ± 10666.460  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482451.288   ± 6257.431  ops/s
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
