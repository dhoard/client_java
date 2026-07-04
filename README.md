# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-04T06:51:29Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.17K | ± 989.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.16K | ± 448.98 | ops/s | 1.1x slower |
| prometheusAdd | 45.58K | ± 4.38K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 44.05K | ± 144.38 | ops/s | 1.3x slower |
| simpleclientInc | 6.20K | ± 10.70 | ops/s | 9.5x slower |
| simpleclientAdd | 6.13K | ± 77.29 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.93K | ± 11.34 | ops/s | 10.0x slower |
| openTelemetryIncNoLabels | 5.59K | ± 1.34K | ops/s | 11x slower |
| openTelemetryAdd | 3.96K | ± 934.85 | ops/s | 15x slower |
| openTelemetryInc | 3.81K | ± 142.06 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.72K | ± 1.40K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 58.97 | ops/s | 1.3x slower |
| prometheusNative | 2.98K | ± 238.91 | ops/s | 1.9x slower |
| openTelemetryClassic | 742.87 | ± 33.35 | ops/s | 7.7x slower |
| openTelemetryExponential | 601.09 | ± 16.96 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.43K | ± 187.48 | ops/s | **fastest** |
| prometheusWriteToNull | 27.29K | ± 418.20 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 586.16K | ± 2.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.89K | ± 10.16K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 548.36K | ± 3.48K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 533.95K | ± 5.77K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44049.596    ± 144.381  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3957.584    ± 934.853  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3806.828    ± 142.057  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5591.573   ± 1336.038  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      45582.582   ± 4378.672  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59174.935    ± 989.035  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52158.151    ± 448.982  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6125.567     ± 77.287  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6203.588     ± 10.703  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5932.671     ± 11.339  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        742.869     ± 33.347  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        601.092     ± 16.965  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5722.391   ± 1397.176  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2983.438    ± 238.908  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4375.525     ± 58.969  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27434.349    ± 187.477  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27285.465    ± 418.200  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     533950.655   ± 5768.787  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548355.389   ± 3478.928  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568890.287  ± 10158.420  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     586158.598   ± 2751.318  ops/s
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
