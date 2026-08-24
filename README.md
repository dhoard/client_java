# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-24T04:19:29Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 58.39K | ± 893.79 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.23K | ± 618.46 | ops/s | 1.1x slower |
| prometheusAdd | 45.83K | ± 4.18K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 42.67K | ± 1.44K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 17.18K | ± 99.39 | ops/s | 3.4x slower |
| openTelemetryInc | 13.78K | ± 204.19 | ops/s | 4.2x slower |
| openTelemetryAdd | 12.20K | ± 34.92 | ops/s | 4.8x slower |
| simpleclientInc | 6.09K | ± 180.03 | ops/s | 9.6x slower |
| simpleclientAdd | 6.03K | ± 52.16 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.86K | ± 67.06 | ops/s | 10.0x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.05K | ± 26.90 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.82K | ± 10.38 | ops/s | 2.4x slower |
| prometheusClassic | 5.60K | ± 1.65K | ops/s | 2.5x slower |
| simpleclient | 4.45K | ± 112.21 | ops/s | 3.2x slower |
| prometheusNative | 2.78K | ± 123.32 | ops/s | 5.1x slower |
| openTelemetryClassic | 825.12 | ± 29.25 | ops/s | 17x slower |
| openTelemetryExponential | 703.27 | ± 41.97 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.59K | ± 302.71 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.49K | ± 215.65 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 581.70K | ± 8.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 570.85K | ± 7.24K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 553.01K | ± 4.36K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 538.03K | ± 8.04K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42672.633   ± 1441.348  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12198.663     ± 34.915  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13784.338    ± 204.195  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17183.137     ± 99.387  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      45832.256   ± 4183.653  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58390.674    ± 893.787  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51232.429    ± 618.465  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6026.250     ± 52.156  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6086.640    ± 180.035  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5863.906     ± 67.060  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        825.121     ± 29.250  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        703.270     ± 41.974  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5604.527   ± 1645.283  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14052.955     ± 26.902  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5822.107     ± 10.376  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2782.252    ± 123.324  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4450.144    ± 112.215  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27491.458    ± 215.650  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27593.084    ± 302.709  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     538027.957   ± 8037.655  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     553009.123   ± 4358.048  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     570847.104   ± 7239.924  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581701.421   ± 8268.030  ops/s
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
