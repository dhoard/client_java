# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-17T08:14:47Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.19K | ± 3.15K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.94K | ± 394.08 | ops/s | 1.1x slower |
| prometheusAdd | 49.54K | ± 2.87K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.86K | ± 2.29K | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 48.02 | ops/s | 9.6x slower |
| simpleclientAdd | 6.46K | ± 14.91 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.44K | ± 155.48 | ops/s | 9.8x slower |
| openTelemetryInc | 3.39K | ± 491.89 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.11K | ± 154.83 | ops/s | 20x slower |
| openTelemetryAdd | 2.91K | ± 28.42 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.97K | ± 2.36K | ops/s | **fastest** |
| simpleclient | 4.35K | ± 37.85 | ops/s | 1.4x slower |
| prometheusNative | 3.26K | ± 62.61 | ops/s | 1.8x slower |
| openTelemetryClassic | 746.17 | ± 20.91 | ops/s | 8.0x slower |
| openTelemetryExponential | 671.20 | ± 79.21 | ops/s | 8.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.69K | ± 883.31 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.21K | ± 1.02K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.19K | ± 3.73K | ops/s | **fastest** |
| prometheusWriteToByteArray | 496.79K | ± 2.20K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.89K | ± 4.36K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 472.93K | ± 7.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48859.025   ± 2289.454  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2914.001     ± 28.416  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3392.274    ± 491.890  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3109.612    ± 154.828  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49536.483   ± 2865.032  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63190.904   ± 3152.206  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56939.289    ± 394.079  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6462.810     ± 14.914  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6570.691     ± 48.023  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6437.935    ± 155.479  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        746.167     ± 20.911  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        671.202     ± 79.206  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5973.582   ± 2359.746  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3255.212     ± 62.608  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4346.114     ± 37.848  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23207.197   ± 1024.081  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23685.402    ± 883.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472928.839   ± 7541.561  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478885.121   ± 4357.569  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     496788.713   ± 2200.369  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512194.863   ± 3725.969  ops/s
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
