# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-31T05:42:11Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.62K | ± 667.39 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.44K | ± 696.31 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.54K | ± 1.02K | ops/s | 1.4x slower |
| prometheusAdd | 44.43K | ± 11.42K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.63K | ± 13.19 | ops/s | 10x slower |
| simpleclientInc | 6.58K | ± 215.55 | ops/s | 10x slower |
| simpleclientAdd | 6.10K | ± 344.69 | ops/s | 11x slower |
| openTelemetryAdd | 1.29K | ± 65.35 | ops/s | 52x slower |
| openTelemetryInc | 1.25K | ± 83.58 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.16K | ± 99.77 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.67K | ± 682.65 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 19.82 | ops/s | 1.0x slower |
| prometheusNative | 2.82K | ± 337.35 | ops/s | 1.7x slower |
| openTelemetryClassic | 687.71 | ± 55.84 | ops/s | 6.8x slower |
| openTelemetryExponential | 583.90 | ± 21.72 | ops/s | 8.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.23K | ± 2.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.58K | ± 4.73K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.82K | ± 4.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 461.60K | ± 3.99K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48535.819   ± 1017.479  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1291.022     ± 65.353  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1252.697     ± 83.582  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1159.112     ± 99.770  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      44430.286  ± 11422.900  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66619.366    ± 667.388  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56435.613    ± 696.312  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6096.548    ± 344.691  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6575.320    ± 215.551  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6633.746     ± 13.193  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        687.709     ± 55.836  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.899     ± 21.719  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4669.373    ± 682.650  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2818.756    ± 337.351  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.453     ± 19.822  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     461596.061   ± 3993.380  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475823.253   ± 4335.245  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482584.097   ± 4733.259  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484228.792   ± 2104.390  ops/s
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
