# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-15T04:08:10Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.18K | ± 1.16K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.76K | ± 141.36 | ops/s | 1.2x slower |
| prometheusAdd | 48.76K | ± 971.53 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.15K | ± 277.70 | ops/s | 1.4x slower |
| openTelemetryIncNoLabels | 17.16K | ± 123.07 | ops/s | 3.5x slower |
| openTelemetryInc | 13.98K | ± 193.83 | ops/s | 4.3x slower |
| openTelemetryAdd | 11.95K | ± 247.29 | ops/s | 5.0x slower |
| simpleclientInc | 6.12K | ± 65.71 | ops/s | 9.8x slower |
| simpleclientAdd | 5.94K | ± 173.38 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.90K | ± 7.03 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.05K | ± 17.65 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.81K | ± 21.99 | ops/s | 2.4x slower |
| prometheusClassic | 5.24K | ± 1.69K | ops/s | 2.7x slower |
| simpleclient | 4.60K | ± 38.65 | ops/s | 3.1x slower |
| prometheusNative | 3.04K | ± 227.54 | ops/s | 4.6x slower |
| openTelemetryClassic | 794.25 | ± 52.51 | ops/s | 18x slower |
| openTelemetryExponential | 688.54 | ± 86.21 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.55K | ± 157.47 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.47K | ± 100.46 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 563.38K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 554.97K | ± 2.69K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.22K | ± 4.89K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 519.14K | ± 6.94K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44147.317    ± 277.703  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11951.648    ± 247.286  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13977.534    ± 193.829  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17158.177    ± 123.065  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48761.571    ± 971.530  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60184.577   ± 1156.555  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50762.613    ± 141.359  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5938.239    ± 173.378  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6120.890     ± 65.708  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5899.176      ± 7.034  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        794.252     ± 52.510  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        688.544     ± 86.206  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5244.873   ± 1689.695  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14049.757     ± 17.646  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5810.570     ± 21.994  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3035.443    ± 227.536  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4595.199     ± 38.648  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27469.917    ± 100.460  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27552.936    ± 157.472  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519143.411   ± 6940.604  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     530223.957   ± 4886.559  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     554974.364   ± 2687.371  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     563379.934   ± 3601.853  ops/s
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
