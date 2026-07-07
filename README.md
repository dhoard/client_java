# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-07T07:14:37Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.12K | ± 370.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.94K | ± 408.31 | ops/s | 1.2x slower |
| prometheusAdd | 51.60K | ± 161.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.21K | ± 1.50K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 40.66 | ops/s | 10x slower |
| simpleclientAdd | 6.49K | ± 56.49 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 44.56 | ops/s | 10x slower |
| openTelemetryInc | 3.40K | ± 305.47 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.18K | ± 23.75 | ops/s | 21x slower |
| openTelemetryAdd | 3.14K | ± 62.28 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 1.33K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 22.36 | ops/s | 1.2x slower |
| prometheusNative | 2.98K | ± 262.54 | ops/s | 1.8x slower |
| openTelemetryClassic | 782.96 | ± 25.47 | ops/s | 7.0x slower |
| openTelemetryExponential | 689.41 | ± 20.75 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.47K | ± 678.87 | ops/s | **fastest** |
| prometheusWriteToNull | 22.51K | ± 333.32 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 507.48K | ± 3.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 504.44K | ± 2.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.03K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.17K | ± 4.88K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49212.036   ± 1500.602  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3138.835     ± 62.276  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3398.950    ± 305.473  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3181.509     ± 23.751  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51601.807    ± 161.728  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66124.093    ± 370.587  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56940.779    ± 408.310  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6485.514     ± 56.486  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6561.033     ± 40.657  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.857     ± 44.558  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        782.961     ± 25.468  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        689.413     ± 20.751  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5453.681   ± 1325.019  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2982.195    ± 262.538  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4405.561     ± 22.357  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24471.784    ± 678.869  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22507.825    ± 333.319  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485172.108   ± 4877.014  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487031.020   ± 3554.851  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     504437.541   ± 2274.405  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507479.577   ± 3197.157  ops/s
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
