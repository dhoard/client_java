# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-09T06:16:42Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.15K | ± 553.17 | ops/s | **fastest** |
| prometheusInc | 30.77K | ± 1.19K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.30K | ± 200.79 | ops/s | 1.1x slower |
| prometheusAdd | 28.52K | ± 114.00 | ops/s | 1.1x slower |
| simpleclientInc | 6.88K | ± 112.79 | ops/s | 4.5x slower |
| simpleclientAdd | 6.49K | ± 270.45 | ops/s | 4.8x slower |
| simpleclientNoLabelsInc | 6.44K | ± 205.62 | ops/s | 4.8x slower |
| openTelemetryInc | 2.60K | ± 260.68 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 2.54K | ± 247.40 | ops/s | 12x slower |
| openTelemetryAdd | 2.32K | ± 348.25 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 88.09 | ops/s | **fastest** |
| prometheusClassic | 2.80K | ± 341.02 | ops/s | 1.6x slower |
| prometheusNative | 2.19K | ± 146.14 | ops/s | 2.0x slower |
| openTelemetryClassic | 592.81 | ± 44.89 | ops/s | 7.5x slower |
| openTelemetryExponential | 459.25 | ± 15.38 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.35K | ± 73.66 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.32K | ± 80.30 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 320.31K | ± 1.48K | ops/s | **fastest** |
| prometheusWriteToNull | 319.80K | ± 2.23K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 299.45K | ± 747.75 | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 295.82K | ± 3.03K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29303.810    ± 200.786  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2318.998    ± 348.246  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2604.836    ± 260.676  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2536.595    ± 247.396  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28524.135    ± 114.004  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30765.271   ± 1187.088  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31151.091    ± 553.174  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6487.897    ± 270.450  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6884.209    ± 112.790  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6436.135    ± 205.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        592.814     ± 44.886  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        459.250     ± 15.382  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2804.782    ± 341.016  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2185.693    ± 146.142  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4460.754     ± 88.086  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18316.212     ± 80.300  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18352.295     ± 73.662  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     295817.586   ± 3028.275  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     299447.200    ± 747.745  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     320308.571   ± 1480.630  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     319800.619   ± 2225.467  ops/s
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
