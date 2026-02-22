# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-22T05:22:27Z
- **Commit:** [`f645a80`](https://github.com/dhoard/client_java/commit/f645a80f239985098f703c3a542ba534e28e04de)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.71K | ± 1.47K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.00K | ± 316.06 | ops/s | 1.2x slower |
| prometheusAdd | 51.32K | ± 516.81 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.85K | ± 1.25K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.65K | ± 86.77 | ops/s | 9.9x slower |
| simpleclientInc | 6.61K | ± 151.55 | ops/s | 9.9x slower |
| simpleclientAdd | 6.26K | ± 234.64 | ops/s | 10x slower |
| openTelemetryAdd | 1.44K | ± 247.68 | ops/s | 46x slower |
| openTelemetryIncNoLabels | 1.21K | ± 28.24 | ops/s | 54x slower |
| openTelemetryInc | 1.17K | ± 15.31 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.29K | ± 553.30 | ops/s | **fastest** |
| simpleclient | 4.48K | ± 57.30 | ops/s | 1.2x slower |
| prometheusNative | 2.85K | ± 328.42 | ops/s | 1.9x slower |
| openTelemetryClassic | 624.71 | ± 26.37 | ops/s | 8.5x slower |
| openTelemetryExponential | 556.70 | ± 24.36 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 499.57K | ± 1.50K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.22K | ± 2.78K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.79K | ± 1.25K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 483.91K | ± 3.74K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48845.215   ± 1250.948  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1439.538    ± 247.675  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1174.159     ± 15.309  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1213.663     ± 28.236  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51318.501    ± 516.805  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65710.392   ± 1473.694  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57003.978    ± 316.064  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6263.142    ± 234.645  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6609.510    ± 151.545  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6653.315     ± 86.768  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        624.706     ± 26.365  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.696     ± 24.356  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5286.136    ± 553.301  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2852.514    ± 328.418  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4479.474     ± 57.300  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483914.350   ± 3738.886  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485794.407   ± 1250.468  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495217.338   ± 2775.262  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499570.207   ± 1502.766  ops/s
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
