# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-27T05:40:14Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.33K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.90K | ± 509.40 | ops/s | 1.1x slower |
| prometheusAdd | 51.82K | ± 123.62 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.34K | ± 2.14K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.57K | ± 110.45 | ops/s | 9.9x slower |
| simpleclientInc | 6.56K | ± 171.62 | ops/s | 10.0x slower |
| simpleclientAdd | 6.52K | ± 28.65 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 233.50 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.33K | ± 115.89 | ops/s | 49x slower |
| openTelemetryAdd | 1.25K | ± 91.36 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.25K | ± 239.69 | ops/s | **fastest** |
| simpleclient | 4.54K | ± 70.68 | ops/s | 1.6x slower |
| prometheusNative | 2.78K | ± 250.05 | ops/s | 2.6x slower |
| openTelemetryClassic | 662.27 | ± 7.84 | ops/s | 11x slower |
| openTelemetryExponential | 549.58 | ± 29.78 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.05K | ± 1.45K | ops/s | **fastest** |
| openMetricsWriteToNull | 490.03K | ± 2.04K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 487.10K | ± 3.48K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.89K | ± 3.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48343.883   ± 2140.046  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1246.973     ± 91.361  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1364.739    ± 233.503  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1334.406    ± 115.895  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51824.988    ± 123.615  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65332.647   ± 1421.841  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56895.646    ± 509.401  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6521.762     ± 28.650  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6563.979    ± 171.617  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6568.764    ± 110.452  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        662.265      ± 7.842  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        549.581     ± 29.781  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7252.349    ± 239.691  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2782.139    ± 250.045  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4540.253     ± 70.677  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482887.419   ± 3663.359  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490029.874   ± 2039.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487104.514   ± 3481.280  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492050.485   ± 1449.294  ops/s
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
