# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-03T08:00:22Z
- **Commit:** [`ab37635`](https://github.com/dhoard/client_java/commit/ab3763518ee1d5d95f5cd2580cacbd4f4be7ac8d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.58K | ± 987.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.37K | ± 148.64 | ops/s | 1.1x slower |
| prometheusAdd | 51.48K | ± 283.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.64K | ± 1.29K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 21.32 | ops/s | 9.8x slower |
| simpleclientAdd | 6.46K | ± 10.80 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.37K | ± 29.86 | ops/s | 10x slower |
| openTelemetryAdd | 3.26K | ± 292.32 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.07K | ± 41.82 | ops/s | 21x slower |
| openTelemetryInc | 3.06K | ± 225.24 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.20K | ± 1.70K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 57.08 | ops/s | 1.4x slower |
| prometheusNative | 3.20K | ± 103.37 | ops/s | 1.9x slower |
| openTelemetryClassic | 770.26 | ± 7.13 | ops/s | 8.0x slower |
| openTelemetryExponential | 650.30 | ± 73.62 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 22.92K | ± 815.37 | ops/s | **fastest** |
| openMetricsWriteToNull | 22.66K | ± 366.04 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 506.21K | ± 4.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.28K | ± 5.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.45K | ± 3.53K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.81K | ± 7.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47637.661   ± 1286.642  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3258.730    ± 292.324  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3057.560    ± 225.236  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3068.706     ± 41.817  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51477.261    ± 283.850  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64582.280    ± 987.536  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56374.906    ± 148.636  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6459.196     ± 10.798  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.474     ± 21.319  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6374.957     ± 29.858  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        770.260      ± 7.133  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        650.298     ± 73.618  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6200.202   ± 1703.453  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3196.226    ± 103.374  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4429.170     ± 57.078  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22664.898    ± 366.042  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22924.933    ± 815.366  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476810.206   ± 7610.208  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485447.214   ± 3534.298  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496278.949   ± 5287.811  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     506211.886   ± 4568.588  ops/s
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
