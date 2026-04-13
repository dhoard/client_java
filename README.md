# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-13T06:04:43Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 454.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.88K | ± 281.03 | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 199.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.70K | ± 1.90K | ops/s | 1.4x slower |
| simpleclientInc | 6.64K | ± 101.19 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.39K | ± 180.59 | ops/s | 10x slower |
| simpleclientAdd | 6.05K | ± 94.62 | ops/s | 11x slower |
| openTelemetryAdd | 1.44K | ± 156.58 | ops/s | 46x slower |
| openTelemetryInc | 1.27K | ± 9.56 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.25K | ± 37.71 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.17K | ± 1.35K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 9.39 | ops/s | 1.4x slower |
| prometheusNative | 2.96K | ± 265.95 | ops/s | 2.1x slower |
| openTelemetryClassic | 673.30 | ± 15.71 | ops/s | 9.2x slower |
| openTelemetryExponential | 555.69 | ± 29.94 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 489.22K | ± 1.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.35K | ± 2.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.03K | ± 9.22K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.41K | ± 3.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48703.329   ± 1899.209  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1435.003    ± 156.580  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1267.564      ± 9.558  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1251.535     ± 37.710  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51206.436    ± 199.434  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66399.804    ± 454.756  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56876.397    ± 281.026  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6045.583     ± 94.622  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6644.924    ± 101.185  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6393.031    ± 180.585  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        673.304     ± 15.714  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.692     ± 29.938  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6173.961   ± 1347.965  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2961.514    ± 265.954  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4407.403      ± 9.393  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473409.015   ± 3004.762  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475026.969   ± 9218.977  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487347.957   ± 2009.262  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     489220.644   ± 1857.797  ops/s
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
