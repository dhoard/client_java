# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-02T07:43:58Z
- **Commit:** [`9c3b097`](https://github.com/dhoard/client_java/commit/9c3b097f6842ffc08fb3a2ed00217c73a6c2b191)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.11K | ± 832.69 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.51K | ± 838.46 | ops/s | 1.1x slower |
| prometheusAdd | 48.54K | ± 73.36 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.37K | ± 1.34K | ops/s | 1.3x slower |
| simpleclientInc | 6.12K | ± 36.09 | ops/s | 9.5x slower |
| simpleclientAdd | 5.94K | ± 269.37 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.89K | ± 10.55 | ops/s | 9.9x slower |
| openTelemetryInc | 5.24K | ± 1.02K | ops/s | 11x slower |
| openTelemetryIncNoLabels | 5.06K | ± 974.47 | ops/s | 11x slower |
| openTelemetryAdd | 4.07K | ± 808.33 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.41K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 51.71 | ops/s | 1.3x slower |
| prometheusNative | 2.98K | ± 161.70 | ops/s | 1.8x slower |
| openTelemetryClassic | 715.27 | ± 15.99 | ops/s | 7.6x slower |
| openTelemetryExponential | 545.43 | ± 12.42 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.54K | ± 194.81 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.42K | ± 163.89 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 555.18K | ± 5.04K | ops/s | **fastest** |
| prometheusWriteToByteArray | 553.80K | ± 6.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.50K | ± 7.81K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 518.17K | ± 3.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43370.630   ± 1340.523  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4072.460    ± 808.329  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5237.267   ± 1017.267  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5058.860    ± 974.475  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48535.436     ± 73.360  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58109.437    ± 832.693  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51512.077    ± 838.464  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5938.523    ± 269.371  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6122.480     ± 36.092  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5887.166     ± 10.548  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.268     ± 15.994  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        545.430     ± 12.418  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5410.553   ± 1586.816  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2983.447    ± 161.698  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4193.272     ± 51.710  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27418.640    ± 163.895  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27536.043    ± 194.811  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518170.062   ± 3495.487  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531495.820   ± 7812.498  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     553803.376   ± 6827.945  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     555176.767   ± 5043.640  ops/s
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
