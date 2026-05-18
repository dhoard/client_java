# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-18T07:19:33Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.76K | ± 1.99K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.48K | ± 511.59 | ops/s | 1.1x slower |
| prometheusAdd | 48.59K | ± 1.03K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.20K | ± 1.28K | ops/s | 1.3x slower |
| simpleclientInc | 6.23K | ± 111.21 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 5.90K | ± 22.30 | ops/s | 9.8x slower |
| simpleclientAdd | 5.62K | ± 109.39 | ops/s | 10x slower |
| openTelemetryInc | 4.60K | ± 1.09K | ops/s | 13x slower |
| openTelemetryIncNoLabels | 3.98K | ± 250.10 | ops/s | 15x slower |
| openTelemetryAdd | 3.42K | ± 107.19 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.57K | ± 55.59 | ops/s | **fastest** |
| prometheusClassic | 4.38K | ± 356.48 | ops/s | 1.0x slower |
| prometheusNative | 2.93K | ± 199.03 | ops/s | 1.6x slower |
| openTelemetryClassic | 715.37 | ± 24.11 | ops/s | 6.4x slower |
| openTelemetryExponential | 539.60 | ± 30.39 | ops/s | 8.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.48K | ± 144.26 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.99K | ± 522.65 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 553.59K | ± 16.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 553.22K | ± 2.33K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.49K | ± 6.14K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 513.68K | ± 6.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43203.884   ± 1281.131  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3422.847    ± 107.187  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4598.744   ± 1087.008  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3976.131    ± 250.104  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48588.951   ± 1030.373  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57764.896   ± 1991.247  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51482.753    ± 511.588  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5624.609    ± 109.389  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6231.494    ± 111.205  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5897.250     ± 22.299  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        715.367     ± 24.109  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.603     ± 30.386  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4378.823    ± 356.481  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2932.152    ± 199.030  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4568.815     ± 55.586  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26990.503    ± 522.649  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27475.772    ± 144.263  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513683.802   ± 6831.357  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531494.072   ± 6137.677  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     553217.124   ± 2329.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553586.040  ± 16667.677  ops/s
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
