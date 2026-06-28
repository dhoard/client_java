# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-28T07:24:45Z
- **Commit:** [`2a2c73d`](https://github.com/dhoard/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.22K | ± 3.99K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.27K | ± 296.86 | ops/s | 1.1x slower |
| prometheusAdd | 51.13K | ± 95.45 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.37K | ± 152.17 | ops/s | 1.3x slower |
| simpleclientInc | 6.59K | ± 7.98 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.36K | ± 37.96 | ops/s | 9.9x slower |
| simpleclientAdd | 6.29K | ± 269.58 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.23K | ± 150.27 | ops/s | 20x slower |
| openTelemetryInc | 3.16K | ± 257.35 | ops/s | 20x slower |
| openTelemetryAdd | 3.04K | ± 292.51 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.95K | ± 1.27K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 72.48 | ops/s | 1.1x slower |
| prometheusNative | 3.13K | ± 69.61 | ops/s | 1.6x slower |
| openTelemetryClassic | 757.88 | ± 14.21 | ops/s | 6.5x slower |
| openTelemetryExponential | 589.87 | ± 92.03 | ops/s | 8.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.19K | ± 246.64 | ops/s | **fastest** |
| prometheusWriteToNull | 23.12K | ± 858.01 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.16K | ± 5.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 497.85K | ± 4.94K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.36K | ± 3.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.55K | ± 3.79K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47369.516    ± 152.174  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3039.680    ± 292.508  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3161.507    ± 257.350  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3229.774    ± 150.269  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51128.861     ± 95.447  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63224.480   ± 3992.409  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56270.125    ± 296.859  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6289.116    ± 269.576  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6593.261      ± 7.977  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.634     ± 37.956  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        757.882     ± 14.206  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        589.866     ± 92.029  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4947.864   ± 1273.763  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3130.542     ± 69.609  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4435.830     ± 72.478  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23186.143    ± 246.643  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23123.184    ± 858.007  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476545.760   ± 3790.168  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481362.261   ± 3633.659  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     497853.655   ± 4935.454  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502160.081   ± 5736.926  ops/s
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
