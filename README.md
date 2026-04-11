# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-11T05:26:15Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.19K | ± 1.13K | ops/s | **fastest** |
| prometheusAdd | 48.53K | ± 1.04K | ops/s | 1.2x slower |
| prometheusNoLabelsInc | 48.34K | ± 2.03K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.93K | ± 1.49K | ops/s | 1.4x slower |
| simpleclientInc | 6.27K | ± 14.27 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.12K | ± 182.35 | ops/s | 9.8x slower |
| simpleclientAdd | 6.03K | ± 255.98 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 1.31K | ± 156.45 | ops/s | 46x slower |
| openTelemetryInc | 1.28K | ± 125.26 | ops/s | 47x slower |
| openTelemetryAdd | 1.26K | ± 9.48 | ops/s | 48x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.06K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 61.06 | ops/s | 1.3x slower |
| prometheusNative | 3.05K | ± 222.92 | ops/s | 2.0x slower |
| openTelemetryClassic | 595.44 | ± 8.53 | ops/s | 10x slower |
| openTelemetryExponential | 526.82 | ± 26.95 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 557.83K | ± 3.37K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.76K | ± 7.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 534.02K | ± 7.34K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 508.81K | ± 22.15K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42927.062   ± 1486.214  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1255.575      ± 9.478  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1278.479    ± 125.256  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1309.502    ± 156.451  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48533.096   ± 1044.794  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60193.867   ± 1130.800  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      48335.494   ± 2025.621  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6031.697    ± 255.984  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6266.335     ± 14.272  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6120.224    ± 182.352  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.437      ± 8.529  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        526.825     ± 26.949  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6063.965   ± 1492.257  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3048.343    ± 222.919  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4551.373     ± 61.064  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     508812.011  ± 22145.724  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     534016.186   ± 7338.109  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545763.515   ± 7344.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557830.310   ± 3369.455  ops/s
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
