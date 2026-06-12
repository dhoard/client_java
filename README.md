# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-12T07:40:52Z
- **Commit:** [`8f8cb84`](https://github.com/dhoard/client_java/commit/8f8cb844283d6288bb83967db9c99c7e8ba7051a)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.00K | ± 912.24 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.65K | ± 257.78 | ops/s | 1.2x slower |
| prometheusAdd | 51.05K | ± 331.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.78K | ± 7.24K | ops/s | 1.5x slower |
| simpleclientInc | 6.58K | ± 12.27 | ops/s | 10x slower |
| simpleclientAdd | 6.37K | ± 108.32 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 33.05 | ops/s | 10x slower |
| openTelemetryInc | 3.64K | ± 89.05 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.20K | ± 176.37 | ops/s | 21x slower |
| openTelemetryAdd | 3.00K | ± 304.22 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.37K | ± 22.90 | ops/s | **fastest** |
| prometheusClassic | 4.33K | ± 76.78 | ops/s | 1.0x slower |
| prometheusNative | 2.80K | ± 316.27 | ops/s | 1.6x slower |
| openTelemetryClassic | 721.37 | ± 27.43 | ops/s | 6.1x slower |
| openTelemetryExponential | 661.18 | ± 15.51 | ops/s | 6.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.92K | ± 534.74 | ops/s | **fastest** |
| prometheusWriteToNull | 23.30K | ± 419.33 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 502.76K | ± 7.63K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.33K | ± 6.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.13K | ± 8.74K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 467.01K | ± 4.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44778.279   ± 7235.521  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2996.144    ± 304.218  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3641.421     ± 89.046  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3204.312    ± 176.374  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51051.793    ± 331.880  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65997.562    ± 912.241  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56651.021    ± 257.781  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6371.221    ± 108.321  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6583.809     ± 12.271  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6355.688     ± 33.050  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        721.372     ± 27.430  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        661.178     ± 15.508  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4329.475     ± 76.780  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2801.824    ± 316.272  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4373.607     ± 22.899  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23921.430    ± 534.741  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23297.628    ± 419.335  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467006.031   ± 4279.906  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478131.344   ± 8742.567  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492327.903   ± 6880.604  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     502762.927   ± 7633.112  ops/s
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
