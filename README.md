# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-02T05:19:01Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 166.81 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.09K | ± 2.23K | ops/s | 1.2x slower |
| prometheusAdd | 50.93K | ± 710.21 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.04K | ± 647.45 | ops/s | 1.3x slower |
| simpleclientInc | 6.77K | ± 22.63 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.54K | ± 109.12 | ops/s | 10x slower |
| simpleclientAdd | 6.03K | ± 169.51 | ops/s | 11x slower |
| openTelemetryAdd | 1.41K | ± 218.71 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.23K | ± 29.69 | ops/s | 54x slower |
| openTelemetryInc | 1.22K | ± 35.87 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.29K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.37K | ± 152.27 | ops/s | 1.4x slower |
| prometheusNative | 2.90K | ± 302.62 | ops/s | 2.2x slower |
| openTelemetryClassic | 688.56 | ± 40.41 | ops/s | 9.1x slower |
| openTelemetryExponential | 549.25 | ± 10.68 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.80K | ± 3.29K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.78K | ± 3.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.42K | ± 5.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.97K | ± 6.14K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50041.734    ± 647.450  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1411.831    ± 218.711  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1220.160     ± 35.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1229.450     ± 29.695  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50926.437    ± 710.206  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65821.561    ± 166.815  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55089.004   ± 2229.897  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6033.087    ± 169.513  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6767.275     ± 22.635  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.362    ± 109.115  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.563     ± 40.406  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.249     ± 10.679  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6290.923   ± 1627.691  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2904.274    ± 302.625  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4367.801    ± 152.273  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467967.570   ± 6138.601  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482424.505   ± 5805.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485777.038   ± 3841.154  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497802.062   ± 3291.256  ops/s
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
