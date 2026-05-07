# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-07T06:36:49Z
- **Commit:** [`0d33b2a`](https://github.com/dhoard/client_java/commit/0d33b2a21208a58f0c67c0e9a9b662044ded45d2)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.95K | ± 211.10 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.89K | ± 932.01 | ops/s | 1.2x slower |
| prometheusAdd | 63.08K | ± 929.14 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.73K | ± 630.29 | ops/s | 1.4x slower |
| simpleclientInc | 7.98K | ± 143.25 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 7.69K | ± 208.76 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 7.57K | ± 184.39 | ops/s | 10x slower |
| simpleclientAdd | 7.51K | ± 23.64 | ops/s | 10x slower |
| openTelemetryInc | 5.47K | ± 136.43 | ops/s | 14x slower |
| openTelemetryAdd | 5.12K | ± 985.03 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.52K | ± 3.13K | ops/s | **fastest** |
| simpleclient | 5.41K | ± 26.46 | ops/s | 1.4x slower |
| prometheusNative | 4.11K | ± 104.56 | ops/s | 1.8x slower |
| openTelemetryClassic | 903.10 | ± 20.06 | ops/s | 8.3x slower |
| openTelemetryExponential | 693.53 | ± 15.29 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 674.88K | ± 3.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 658.01K | ± 4.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 654.82K | ± 6.20K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 634.14K | ± 5.29K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56725.339    ± 630.294  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5120.046    ± 985.026  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5466.717    ± 136.427  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7571.339    ± 184.390  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63079.941    ± 929.143  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76949.405    ± 211.100  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66888.165    ± 932.010  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7511.179     ± 23.637  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7981.298    ± 143.253  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7685.293    ± 208.757  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        903.099     ± 20.057  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        693.529     ± 15.295  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7522.157   ± 3126.770  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4110.970    ± 104.559  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5414.590     ± 26.463  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     634136.617   ± 5294.657  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     654817.372   ± 6202.306  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     658008.809   ± 4852.355  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     674883.439   ± 3604.520  ops/s
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
