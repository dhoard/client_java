# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-17T04:16:24Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 66.17K | ± 297.35 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.97K | ± 1.74K | ops/s | 1.2x slower |
| prometheusAdd | 51.41K | ± 152.95 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.27K | ± 1.69K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 18.48K | ± 192.12 | ops/s | 3.6x slower |
| openTelemetryInc | 14.52K | ± 863.77 | ops/s | 4.6x slower |
| openTelemetryAdd | 12.93K | ± 130.78 | ops/s | 5.1x slower |
| simpleclientInc | 6.56K | ± 35.78 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.45K | ± 134.57 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 260.81 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.29K | ± 18.54 | ops/s | **fastest** |
| prometheusClassic | 5.96K | ± 733.85 | ops/s | 2.1x slower |
| prometheusClassicSingleThread | 4.57K | ± 37.19 | ops/s | 2.7x slower |
| simpleclient | 4.40K | ± 20.42 | ops/s | 2.8x slower |
| prometheusNative | 2.57K | ± 88.66 | ops/s | 4.8x slower |
| openTelemetryExponential | 881.14 | ± 179.60 | ops/s | 14x slower |
| openTelemetryClassic | 838.10 | ± 50.01 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.16K | ± 218.09 | ops/s | **fastest** |
| prometheusWriteToNull | 23.27K | ± 796.24 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 508.63K | ± 2.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 500.85K | ± 2.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.09K | ± 3.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 477.80K | ± 2.64K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48265.997   ± 1692.487  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12928.750    ± 130.782  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14517.166    ± 863.767  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18478.348    ± 192.123  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51408.984    ± 152.953  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66173.735    ± 297.346  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55974.840   ± 1740.739  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6289.934    ± 260.814  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6555.935     ± 35.776  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6447.595    ± 134.566  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        838.104     ± 50.012  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        881.138    ± 179.603  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5958.547    ± 733.847  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12286.169     ± 18.544  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4571.743     ± 37.185  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2566.823     ± 88.656  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4395.813     ± 20.416  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24164.976    ± 218.095  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23268.121    ± 796.242  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477799.738   ± 2635.668  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481087.293   ± 3782.098  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500852.869   ± 2020.598  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     508632.159   ± 2297.084  ops/s
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
