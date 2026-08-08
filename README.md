# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-08T04:40:52Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.09K | ± 182.67 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.82K | ± 779.51 | ops/s | 1.1x slower |
| prometheusAdd | 48.24K | ± 347.22 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.75K | ± 1.66K | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 17.11K | ± 137.15 | ops/s | 3.5x slower |
| openTelemetryInc | 13.56K | ± 263.35 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.17K | ± 93.66 | ops/s | 4.9x slower |
| simpleclientInc | 6.16K | ± 67.68 | ops/s | 9.6x slower |
| simpleclientAdd | 5.95K | ± 152.58 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.85K | ± 76.56 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.96K | ± 91.25 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.80K | ± 20.20 | ops/s | 2.4x slower |
| prometheusClassic | 5.35K | ± 366.09 | ops/s | 2.6x slower |
| simpleclient | 4.24K | ± 319.69 | ops/s | 3.3x slower |
| prometheusNative | 2.93K | ± 207.06 | ops/s | 4.8x slower |
| openTelemetryClassic | 780.86 | ± 30.74 | ops/s | 18x slower |
| openTelemetryExponential | 686.72 | ± 36.66 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.41K | ± 217.74 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.36K | ± 274.04 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 542.45K | ± 31.77K | ops/s | **fastest** |
| prometheusWriteToByteArray | 517.22K | ± 2.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.90K | ± 3.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 482.11K | ± 2.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42752.891   ± 1664.630  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12174.663     ± 93.657  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13562.213    ± 263.346  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17113.309    ± 137.149  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48242.880    ± 347.219  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59085.418    ± 182.674  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51823.159    ± 779.510  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5948.589    ± 152.583  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6162.336     ± 67.676  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5848.415     ± 76.560  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        780.858     ± 30.738  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        686.721     ± 36.663  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5351.979    ± 366.086  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13962.100     ± 91.252  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5803.307     ± 20.198  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2927.198    ± 207.060  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4235.937    ± 319.687  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23359.003    ± 274.042  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23414.724    ± 217.739  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482106.087   ± 2727.728  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485904.880   ± 3782.035  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     517217.419   ± 2337.793  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542445.333  ± 31765.160  ops/s
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
