# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-14T05:15:42Z
- **Commit:** [`229e2e0`](https://github.com/dhoard/client_java/commit/229e2e003bd639f3744566940f503d05e8b9ba18)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.42K | ± 308.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.75K | ± 256.47 | ops/s | 1.2x slower |
| prometheusAdd | 51.42K | ± 274.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.56K | ± 1.38K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.64K | ± 95.60 | ops/s | 10x slower |
| simpleclientInc | 6.57K | ± 176.76 | ops/s | 10x slower |
| simpleclientAdd | 6.54K | ± 44.68 | ops/s | 10x slower |
| openTelemetryInc | 1.28K | ± 85.15 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.28K | ± 22.13 | ops/s | 52x slower |
| openTelemetryAdd | 1.25K | ± 5.97 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.25K | ± 1.35K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 54.24 | ops/s | 1.4x slower |
| prometheusNative | 2.78K | ± 241.88 | ops/s | 2.2x slower |
| openTelemetryClassic | 676.20 | ± 31.23 | ops/s | 9.2x slower |
| openTelemetryExponential | 537.40 | ± 16.55 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.56K | ± 4.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 490.14K | ± 5.93K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.55K | ± 5.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 486.01K | ± 2.22K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48563.146   ± 1383.496  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.450      ± 5.973  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1283.919     ± 85.147  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1280.679     ± 22.132  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51417.422    ± 274.418  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66417.688    ± 308.026  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56750.489    ± 256.465  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6536.191     ± 44.678  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6567.945    ± 176.758  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6638.564     ± 95.601  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        676.204     ± 31.229  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.405     ± 16.554  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6248.475   ± 1351.253  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2782.523    ± 241.882  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4521.667     ± 54.236  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486014.936   ± 2218.584  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486546.915   ± 5113.853  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490138.090   ± 5926.318  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502557.689   ± 4182.651  ops/s
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
