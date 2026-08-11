# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-11T04:50:42Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.11K | ± 1.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.84K | ± 256.99 | ops/s | 1.1x slower |
| prometheusAdd | 50.66K | ± 542.92 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.46K | ± 8.17K | ops/s | 1.5x slower |
| openTelemetryIncNoLabels | 18.36K | ± 340.46 | ops/s | 3.5x slower |
| openTelemetryInc | 14.55K | ± 277.93 | ops/s | 4.5x slower |
| openTelemetryAdd | 12.81K | ± 157.21 | ops/s | 5.1x slower |
| simpleclientInc | 6.49K | ± 17.62 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.36K | ± 8.82 | ops/s | 10x slower |
| simpleclientAdd | 5.97K | ± 388.25 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.28K | ± 45.86 | ops/s | **fastest** |
| prometheusClassic | 5.45K | ± 615.99 | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 4.55K | ± 31.83 | ops/s | 2.7x slower |
| simpleclient | 4.43K | ± 98.87 | ops/s | 2.8x slower |
| prometheusNative | 3.03K | ± 319.55 | ops/s | 4.1x slower |
| openTelemetryExponential | 864.68 | ± 80.15 | ops/s | 14x slower |
| openTelemetryClassic | 812.87 | ± 109.52 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.11K | ± 529.64 | ops/s | **fastest** |
| prometheusWriteToNull | 23.85K | ± 410.36 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 504.39K | ± 2.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 503.79K | ± 4.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 482.68K | ± 5.23K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 474.75K | ± 8.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44456.201   ± 8168.092  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12813.268    ± 157.211  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14548.907    ± 277.926  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18363.056    ± 340.458  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50662.618    ± 542.917  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65110.125   ± 1179.496  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56838.017    ± 256.995  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5974.897    ± 388.246  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6494.397     ± 17.619  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6356.612      ± 8.823  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        812.873    ± 109.521  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        864.679     ± 80.148  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5453.371    ± 615.992  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12278.320     ± 45.859  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4549.100     ± 31.827  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3026.035    ± 319.552  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4427.875     ± 98.871  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24114.602    ± 529.641  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23846.646    ± 410.358  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     474753.396   ± 8112.723  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482679.512   ± 5231.510  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     503792.805   ± 4285.326  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504392.082   ± 2751.585  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
