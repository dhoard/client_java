# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-02T06:06:13Z
- **Commit:** [`188e434`](https://github.com/dhoard/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.86K | ± 128.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.28K | ± 545.29 | ops/s | 1.1x slower |
| prometheusAdd | 48.33K | ± 286.42 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.02K | ± 1.14K | ops/s | 1.4x slower |
| simpleclientInc | 6.25K | ± 126.13 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.10K | ± 272.87 | ops/s | 9.8x slower |
| simpleclientAdd | 5.91K | ± 231.99 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.53K | ± 519.98 | ops/s | 11x slower |
| openTelemetryAdd | 5.17K | ± 21.07 | ops/s | 12x slower |
| openTelemetryInc | 4.72K | ± 944.92 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.32K | ± 659.28 | ops/s | **fastest** |
| simpleclient | 4.22K | ± 43.92 | ops/s | 1.0x slower |
| prometheusNative | 2.96K | ± 286.87 | ops/s | 1.5x slower |
| openTelemetryClassic | 756.24 | ± 32.60 | ops/s | 5.7x slower |
| openTelemetryExponential | 550.14 | ± 23.45 | ops/s | 7.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 561.23K | ± 4.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 553.65K | ± 4.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.82K | ± 1.94K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 525.09K | ± 8.39K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43021.699   ± 1142.689  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5168.853     ± 21.073  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4718.934    ± 944.916  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5534.929    ± 519.984  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48325.934    ± 286.419  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59861.729    ± 128.207  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52282.918    ± 545.287  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5910.808    ± 231.992  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6247.035    ± 126.128  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6096.093    ± 272.865  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        756.244     ± 32.602  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        550.142     ± 23.451  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4315.234    ± 659.277  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2962.356    ± 286.865  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4224.000     ± 43.923  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     525088.275   ± 8388.943  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     530817.630   ± 1943.700  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     553652.006   ± 4308.392  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     561225.612   ± 4918.105  ops/s
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
