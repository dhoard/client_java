# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-08T05:42:45Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.07K | ± 369.23 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.09K | ± 173.33 | ops/s | 1.2x slower |
| prometheusAdd | 51.33K | ± 151.25 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.88K | ± 1.18K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 204.91 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.42K | ± 159.46 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 156.67 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 225.35 | ops/s | 46x slower |
| openTelemetryInc | 1.31K | ± 68.02 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.23K | ± 42.68 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.70K | ± 448.46 | ops/s | **fastest** |
| simpleclient | 4.39K | ± 56.55 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 287.55 | ops/s | 1.6x slower |
| openTelemetryClassic | 704.97 | ± 16.40 | ops/s | 6.7x slower |
| openTelemetryExponential | 543.69 | ± 30.03 | ops/s | 8.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.30K | ± 2.03K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.00K | ± 3.22K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.71K | ± 1.88K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.56K | ± 2.74K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48881.134   ± 1182.457  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1444.213    ± 225.350  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1312.356     ± 68.015  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1234.336     ± 42.677  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51325.492    ± 151.252  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66069.390    ± 369.231  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57093.006    ± 173.335  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6306.344    ± 156.671  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.892    ± 204.909  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6418.912    ± 159.456  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.971     ± 16.401  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.694     ± 30.033  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4702.770    ± 448.461  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2940.179    ± 287.554  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4390.550     ± 56.553  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486564.611   ± 2737.482  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486713.119   ± 1877.128  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491001.278   ± 3224.548  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492304.135   ± 2030.607  ops/s
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
