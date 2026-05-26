# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-26T07:14:51Z
- **Commit:** [`5ee188f`](https://github.com/dhoard/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.23K | ± 3.47K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.21K | ± 454.35 | ops/s | 1.1x slower |
| prometheusAdd | 48.51K | ± 20.40 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.35K | ± 284.21 | ops/s | 1.3x slower |
| simpleclientInc | 6.09K | ± 8.57 | ops/s | 9.4x slower |
| simpleclientAdd | 6.05K | ± 178.95 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.86K | ± 41.96 | ops/s | 9.8x slower |
| openTelemetryInc | 5.07K | ± 1.07K | ops/s | 11x slower |
| openTelemetryIncNoLabels | 4.72K | ± 937.04 | ops/s | 12x slower |
| openTelemetryAdd | 3.89K | ± 789.51 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.91K | ± 3.15K | ops/s | **fastest** |
| simpleclient | 4.50K | ± 103.57 | ops/s | 1.5x slower |
| prometheusNative | 2.90K | ± 288.58 | ops/s | 2.4x slower |
| openTelemetryClassic | 713.16 | ± 26.68 | ops/s | 9.7x slower |
| openTelemetryExponential | 541.71 | ± 13.53 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.72K | ± 65.36 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.84K | ± 284.84 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.74K | ± 2.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 557.41K | ± 15.47K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.49K | ± 8.33K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 536.39K | ± 7.82K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44346.925    ± 284.212  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3886.601    ± 789.505  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5065.202   ± 1071.870  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4720.789    ± 937.040  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48514.133     ± 20.398  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57233.401   ± 3469.360  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52214.115    ± 454.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6050.646    ± 178.951  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6090.971      ± 8.571  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5861.636     ± 41.962  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        713.155     ± 26.685  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        541.713     ± 13.528  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6909.698   ± 3147.139  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2904.079    ± 288.581  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4497.262    ± 103.565  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26837.128    ± 284.840  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27721.056     ± 65.359  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536393.974   ± 7824.775  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546488.267   ± 8326.205  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     557413.362  ± 15471.416  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581744.980   ± 2962.965  ops/s
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
