# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-14T06:56:45Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.70K | ± 500.51 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.85K | ± 309.40 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 173.20 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.26K | ± 1.75K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 12.24 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 25.07 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.34K | ± 8.99 | ops/s | 11x slower |
| openTelemetryAdd | 3.35K | ± 428.52 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.21K | ± 383.78 | ops/s | 21x slower |
| openTelemetryInc | 3.10K | ± 138.75 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.14K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 60.18 | ops/s | 1.2x slower |
| prometheusNative | 2.90K | ± 200.42 | ops/s | 1.8x slower |
| openTelemetryClassic | 756.98 | ± 19.23 | ops/s | 6.8x slower |
| openTelemetryExponential | 688.29 | ± 94.73 | ops/s | 7.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.03K | ± 547.76 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.68K | ± 1.02K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 512.85K | ± 3.71K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.30K | ± 2.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 484.58K | ± 3.48K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 482.64K | ± 2.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49260.390   ± 1752.608  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3350.361    ± 428.521  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3104.413    ± 138.751  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3213.519    ± 383.783  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51290.810    ± 173.199  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66700.683    ± 500.510  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56851.920    ± 309.396  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6444.116     ± 25.069  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.333     ± 12.236  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6335.435      ± 8.994  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        756.979     ± 19.231  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        688.286     ± 94.731  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5143.484   ± 1592.891  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2899.502    ± 200.415  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4425.810     ± 60.177  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23676.915   ± 1022.720  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24025.139    ± 547.763  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482641.460   ± 2540.769  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484575.870   ± 3483.794  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503300.231   ± 2122.641  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     512845.502   ± 3707.910  ops/s
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
