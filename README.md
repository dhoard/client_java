# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-13T06:57:22Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.24K | ± 81.43 | ops/s | **fastest** |
| prometheusInc | 31.24K | ± 507.10 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.54K | ± 497.24 | ops/s | 1.1x slower |
| prometheusAdd | 28.40K | ± 36.95 | ops/s | 1.1x slower |
| simpleclientInc | 6.87K | ± 99.27 | ops/s | 4.5x slower |
| simpleclientNoLabelsInc | 6.71K | ± 213.59 | ops/s | 4.7x slower |
| simpleclientAdd | 6.55K | ± 133.55 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 2.80K | ± 199.82 | ops/s | 11x slower |
| openTelemetryInc | 2.59K | ± 249.53 | ops/s | 12x slower |
| openTelemetryAdd | 2.39K | ± 24.26 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.53K | ± 58.44 | ops/s | **fastest** |
| prometheusClassic | 2.43K | ± 152.56 | ops/s | 1.9x slower |
| prometheusNative | 2.08K | ± 323.28 | ops/s | 2.2x slower |
| openTelemetryClassic | 581.05 | ± 43.08 | ops/s | 7.8x slower |
| openTelemetryExponential | 499.97 | ± 16.67 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.25K | ± 96.91 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.17K | ± 91.69 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 315.59K | ± 1.74K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.55K | ± 1.58K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 293.16K | ± 2.36K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 291.42K | ± 2.65K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28543.104    ± 497.239  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2387.464     ± 24.258  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2589.140    ± 249.529  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2798.509    ± 199.818  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28403.564     ± 36.949  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31241.251    ± 507.098  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31242.919     ± 81.426  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6545.182    ± 133.555  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6868.331     ± 99.272  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6711.056    ± 213.595  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        581.051     ± 43.081  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        499.971     ± 16.671  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2434.405    ± 152.556  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2078.999    ± 323.279  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4533.833     ± 58.438  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18169.237     ± 91.687  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18253.392     ± 96.907  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     291415.475   ± 2649.712  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     293161.052   ± 2364.832  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315552.780   ± 1582.463  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     315587.924   ± 1738.456  ops/s
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
