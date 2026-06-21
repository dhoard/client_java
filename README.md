# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-21T07:58:39Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.37K | ± 257.27 | ops/s | **fastest** |
| prometheusInc | 30.46K | ± 842.99 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 29.73K | ± 814.67 | ops/s | 1.1x slower |
| prometheusAdd | 28.49K | ± 248.70 | ops/s | 1.1x slower |
| simpleclientInc | 6.87K | ± 121.84 | ops/s | 4.6x slower |
| simpleclientAdd | 6.52K | ± 73.25 | ops/s | 4.8x slower |
| simpleclientNoLabelsInc | 6.34K | ± 215.37 | ops/s | 4.9x slower |
| openTelemetryInc | 2.57K | ± 339.68 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 2.53K | ± 86.55 | ops/s | 12x slower |
| openTelemetryAdd | 2.25K | ± 192.44 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.46K | ± 121.03 | ops/s | **fastest** |
| prometheusClassic | 2.63K | ± 196.43 | ops/s | 1.7x slower |
| prometheusNative | 2.32K | ± 169.12 | ops/s | 1.9x slower |
| openTelemetryClassic | 615.14 | ± 24.35 | ops/s | 7.2x slower |
| openTelemetryExponential | 462.67 | ± 15.12 | ops/s | 9.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.28K | ± 77.81 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.19K | ± 228.09 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 324.79K | ± 4.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 322.71K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 298.12K | ± 4.25K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 297.59K | ± 3.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29729.666    ± 814.667  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2250.760    ± 192.444  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2568.845    ± 339.685  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2533.359     ± 86.550  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28489.163    ± 248.704  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30459.490    ± 842.985  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31369.679    ± 257.269  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6520.653     ± 73.245  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6866.526    ± 121.841  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6341.140    ± 215.365  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        615.138     ± 24.353  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        462.667     ± 15.119  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2631.976    ± 196.427  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2319.848    ± 169.116  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4459.287    ± 121.034  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18187.523    ± 228.094  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18284.426     ± 77.811  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     298115.073   ± 4250.631  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     297591.351   ± 3399.459  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     322707.506   ± 3097.299  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     324791.018   ± 4062.618  ops/s
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
