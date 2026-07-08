# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-08T06:13:38Z
- **Commit:** [`b0a5e13`](https://github.com/dhoard/client_java/commit/b0a5e13a7546290c74872a8aec62ac5040615e3e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.52K | ± 598.37 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.19K | ± 936.94 | ops/s | 1.2x slower |
| prometheusAdd | 51.07K | ± 646.95 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.53K | ± 1.79K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 41.66 | ops/s | 10.0x slower |
| simpleclientAdd | 6.45K | ± 44.79 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.37K | ± 30.55 | ops/s | 10x slower |
| openTelemetryInc | 3.58K | ± 354.57 | ops/s | 18x slower |
| openTelemetryAdd | 3.43K | ± 381.35 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.24K | ± 266.86 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.56K | ± 712.87 | ops/s | **fastest** |
| simpleclient | 4.13K | ± 385.69 | ops/s | 1.1x slower |
| prometheusNative | 2.95K | ± 322.85 | ops/s | 1.5x slower |
| openTelemetryClassic | 719.41 | ± 30.76 | ops/s | 6.3x slower |
| openTelemetryExponential | 634.10 | ± 28.44 | ops/s | 7.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.60K | ± 370.04 | ops/s | **fastest** |
| prometheusWriteToNull | 24.50K | ± 234.23 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.21K | ± 5.02K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.47K | ± 2.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.68K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.92K | ± 3.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49532.154   ± 1786.019  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3428.104    ± 381.352  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3576.197    ± 354.574  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3235.931    ± 266.862  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51069.122    ± 646.946  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65523.456    ± 598.365  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56192.033    ± 936.945  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6453.442     ± 44.794  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6564.188     ± 41.656  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6366.639     ± 30.554  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.414     ± 30.759  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        634.095     ± 28.435  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4557.529    ± 712.868  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2950.808    ± 322.854  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4129.485    ± 385.687  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24602.233    ± 370.040  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24498.505    ± 234.230  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471920.382   ± 3199.727  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485679.958   ± 3085.804  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493466.820   ± 2992.469  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502213.165   ± 5015.401  ops/s
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
