# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-23T05:27:51Z
- **Commit:** [`f645a80`](https://github.com/dhoard/client_java/commit/f645a80f239985098f703c3a542ba534e28e04de)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.89K | ± 108.16 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 423.93 | ops/s | 1.2x slower |
| prometheusAdd | 50.98K | ± 1.26K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.31K | ± 1.57K | ops/s | 1.4x slower |
| simpleclientInc | 6.64K | ± 140.82 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.45K | ± 211.54 | ops/s | 10x slower |
| simpleclientAdd | 6.28K | ± 241.25 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.35K | ± 229.88 | ops/s | 49x slower |
| openTelemetryAdd | 1.28K | ± 55.12 | ops/s | 52x slower |
| openTelemetryInc | 1.26K | ± 47.73 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 57.88 | ops/s | **fastest** |
| prometheusClassic | 4.22K | ± 183.92 | ops/s | 1.1x slower |
| prometheusNative | 2.85K | ± 331.59 | ops/s | 1.6x slower |
| openTelemetryClassic | 694.07 | ± 35.86 | ops/s | 6.6x slower |
| openTelemetryExponential | 541.07 | ± 25.36 | ops/s | 8.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 494.76K | ± 2.88K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.35K | ± 5.09K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.99K | ± 1.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 478.18K | ± 3.94K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48308.381   ± 1570.688  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1276.814     ± 55.121  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1258.038     ± 47.728  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1345.715    ± 229.883  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50975.449   ± 1258.073  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65885.853    ± 108.156  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56965.151    ± 423.930  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6275.209    ± 241.254  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6636.185    ± 140.821  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6451.446    ± 211.544  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        694.067     ± 35.863  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.067     ± 25.364  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4219.885    ± 183.921  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2851.105    ± 331.587  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4577.150     ± 57.884  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478183.731   ± 3936.559  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483986.062   ± 1985.276  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484352.997   ± 5092.564  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494760.351   ± 2880.656  ops/s
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
