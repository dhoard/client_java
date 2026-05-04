# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-04T06:38:50Z
- **Commit:** [`188e434`](https://github.com/dhoard/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.30K | ± 897.97 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.69K | ± 363.52 | ops/s | 1.2x slower |
| prometheusAdd | 51.34K | ± 119.03 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.08K | ± 988.03 | ops/s | 1.4x slower |
| simpleclientInc | 6.65K | ± 47.99 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.35K | ± 202.58 | ops/s | 10x slower |
| simpleclientAdd | 5.96K | ± 17.92 | ops/s | 11x slower |
| openTelemetryAdd | 3.18K | ± 408.14 | ops/s | 21x slower |
| openTelemetryInc | 3.16K | ± 334.39 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.04K | ± 337.10 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.57K | ± 395.88 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 60.81 | ops/s | 1.0x slower |
| prometheusNative | 2.79K | ± 400.35 | ops/s | 1.6x slower |
| openTelemetryClassic | 767.57 | ± 39.33 | ops/s | 5.9x slower |
| openTelemetryExponential | 665.92 | ± 90.94 | ops/s | 6.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 487.82K | ± 2.07K | ops/s | **fastest** |
| prometheusWriteToNull | 486.73K | ± 3.60K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 478.31K | ± 4.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 468.52K | ± 3.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49078.618    ± 988.031  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3177.893    ± 408.144  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3159.825    ± 334.385  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3037.586    ± 337.100  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51339.048    ± 119.025  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66296.374    ± 897.969  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56690.517    ± 363.517  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5959.025     ± 17.923  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6650.829     ± 47.990  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.804    ± 202.583  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        767.566     ± 39.325  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        665.917     ± 90.941  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4566.873    ± 395.878  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2793.451    ± 400.349  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4431.446     ± 60.814  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     468518.323   ± 3757.660  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478307.107   ± 4800.863  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487823.069   ± 2067.312  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     486726.975   ± 3597.440  ops/s
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
