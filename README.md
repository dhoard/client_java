# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-15T07:02:30Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.83K | ± 50.91 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.52K | ± 964.18 | ops/s | 1.2x slower |
| prometheusAdd | 48.23K | ± 415.90 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.09K | ± 163.69 | ops/s | 1.4x slower |
| simpleclientInc | 6.10K | ± 82.39 | ops/s | 9.8x slower |
| simpleclientAdd | 6.08K | ± 7.73 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.02K | ± 163.91 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 4.95K | ± 1.04K | ops/s | 12x slower |
| openTelemetryInc | 4.49K | ± 1.02K | ops/s | 13x slower |
| openTelemetryAdd | 3.89K | ± 800.85 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.94K | ± 990.30 | ops/s | **fastest** |
| simpleclient | 4.20K | ± 21.01 | ops/s | 1.4x slower |
| prometheusNative | 2.98K | ± 261.00 | ops/s | 2.0x slower |
| openTelemetryClassic | 701.87 | ± 35.69 | ops/s | 8.5x slower |
| openTelemetryExponential | 554.08 | ± 46.65 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.60K | ± 312.45 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.09K | ± 384.33 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 589.13K | ± 2.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 575.38K | ± 3.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 541.66K | ± 10.35K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 529.46K | ± 3.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44087.168    ± 163.690  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3889.726    ± 800.851  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4491.355   ± 1019.185  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4949.859   ± 1042.042  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48232.272    ± 415.896  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59830.896     ± 50.908  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51523.430    ± 964.175  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6082.178      ± 7.727  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6104.842     ± 82.393  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6024.385    ± 163.908  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        701.873     ± 35.686  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.077     ± 46.654  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5938.283    ± 990.299  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2978.567    ± 260.998  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4204.624     ± 21.008  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27091.978    ± 384.331  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27603.212    ± 312.448  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     529464.715   ± 3293.795  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     541657.896  ± 10350.085  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     575384.777   ± 3548.756  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     589130.945   ± 2448.402  ops/s
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
