# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-10T06:44:02Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 56.22K | ± 1.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.22K | ± 450.75 | ops/s | 1.1x slower |
| prometheusAdd | 48.24K | ± 395.54 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.58K | ± 3.17K | ops/s | 1.3x slower |
| simpleclientInc | 6.07K | ± 21.62 | ops/s | 9.3x slower |
| simpleclientNoLabelsInc | 6.05K | ± 198.05 | ops/s | 9.3x slower |
| simpleclientAdd | 6.02K | ± 146.70 | ops/s | 9.3x slower |
| openTelemetryInc | 4.69K | ± 1.18K | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.40K | ± 390.16 | ops/s | 13x slower |
| openTelemetryAdd | 4.03K | ± 748.63 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.85K | ± 1.47K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 58.43 | ops/s | 1.8x slower |
| prometheusNative | 2.76K | ± 113.52 | ops/s | 2.8x slower |
| openTelemetryClassic | 713.25 | ± 2.47 | ops/s | 11x slower |
| openTelemetryExponential | 550.65 | ± 17.77 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.35K | ± 276.44 | ops/s | **fastest** |
| prometheusWriteToNull | 27.08K | ± 177.89 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 584.09K | ± 4.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 571.09K | ± 4.50K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.76K | ± 3.91K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 531.17K | ± 2.30K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42578.043   ± 3174.639  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4030.666    ± 748.627  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4688.184   ± 1183.522  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4401.464    ± 390.163  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48237.089    ± 395.537  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      56221.708   ± 1178.372  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51222.594    ± 450.754  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6018.904    ± 146.697  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6072.069     ± 21.618  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6050.511    ± 198.053  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        713.252      ± 2.468  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.649     ± 17.766  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7853.326   ± 1472.630  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2758.876    ± 113.523  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4419.698     ± 58.429  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27346.339    ± 276.440  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27078.327    ± 177.894  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531170.182   ± 2303.128  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546762.590   ± 3908.100  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     571092.912   ± 4503.058  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     584090.385   ± 4512.049  ops/s
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
