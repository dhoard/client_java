# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-15T05:55:19Z
- **Commit:** [`be2bc20`](https://github.com/dhoard/client_java/commit/be2bc20fdf941be85a0ad020f5f405af623a7883)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 58.46K | ± 1.96K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.46K | ± 1.02K | ops/s | 1.1x slower |
| prometheusAdd | 48.79K | ± 699.43 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.70K | ± 1.52K | ops/s | 1.3x slower |
| simpleclientAdd | 6.06K | ± 178.10 | ops/s | 9.6x slower |
| simpleclientInc | 6.05K | ± 52.58 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.88K | ± 20.55 | ops/s | 10.0x slower |
| openTelemetryInc | 5.47K | ± 1.20K | ops/s | 11x slower |
| openTelemetryAdd | 4.66K | ± 868.05 | ops/s | 13x slower |
| openTelemetryIncNoLabels | 3.82K | ± 168.77 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 5.47K | ± 1.54K | ops/s | **fastest** |
| simpleclient | 4.64K | ± 45.17 | ops/s | 1.2x slower |
| prometheusNative | 3.13K | ± 130.69 | ops/s | 1.7x slower |
| openTelemetryClassic | 733.86 | ± 42.17 | ops/s | 7.4x slower |
| openTelemetryExponential | 594.50 | ± 57.78 | ops/s | 9.2x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 27.03K | ± 230.63 | ops/s | **fastest** |
| prometheusWriteToNull | 26.96K | ± 727.33 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 567.62K | ± 4.18K | ops/s | **fastest** |
| prometheusWriteToByteArray | 554.73K | ± 6.53K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 533.07K | ± 3.63K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 522.35K | ± 3.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43696.512   ± 1517.000  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4656.006    ± 868.047  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5467.963   ± 1203.730  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3818.970    ± 168.769  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48793.669    ± 699.426  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58463.307   ± 1959.316  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51459.384   ± 1024.083  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6061.630    ± 178.100  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6049.343     ± 52.580  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5875.629     ± 20.548  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        733.863     ± 42.173  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.496     ± 57.776  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5466.577   ± 1538.682  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3134.056    ± 130.691  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4644.807     ± 45.167  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27032.776    ± 230.627  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      26963.724    ± 727.327  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     522349.944   ± 3204.350  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     533067.838   ± 3631.479  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     554729.002   ± 6532.241  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     567618.577   ± 4177.996  ops/s
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
