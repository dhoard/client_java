# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-09T05:39:10Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.12K | ± 5.18K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.24K | ± 925.35 | ops/s | 1.1x slower |
| prometheusAdd | 51.67K | ± 273.10 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 47.73K | ± 331.13 | ops/s | 1.3x slower |
| simpleclientInc | 6.57K | ± 206.28 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.34K | ± 238.57 | ops/s | 10.0x slower |
| simpleclientAdd | 6.23K | ± 204.39 | ops/s | 10x slower |
| openTelemetryInc | 1.49K | ± 236.73 | ops/s | 42x slower |
| openTelemetryIncNoLabels | 1.31K | ± 102.71 | ops/s | 48x slower |
| openTelemetryAdd | 1.28K | ± 11.83 | ops/s | 50x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.34K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 42.41 | ops/s | 1.6x slower |
| prometheusNative | 2.75K | ± 335.93 | ops/s | 2.7x slower |
| openTelemetryClassic | 672.30 | ± 7.56 | ops/s | 11x slower |
| openTelemetryExponential | 583.96 | ± 28.00 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.21K | ± 2.50K | ops/s | **fastest** |
| openMetricsWriteToNull | 476.31K | ± 6.75K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 469.71K | ± 7.26K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.53K | ± 7.36K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47729.917    ± 331.133  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1275.033     ± 11.834  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1490.087    ± 236.733  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1308.548    ± 102.706  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51666.432    ± 273.103  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63118.917   ± 5182.994  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56243.502    ± 925.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6228.500    ± 204.392  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6568.855    ± 206.275  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6336.138    ± 238.566  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        672.297      ± 7.563  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.959     ± 27.998  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7343.730   ± 1485.818  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2750.995    ± 335.934  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4461.366     ± 42.407  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467526.069   ± 7360.245  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476310.093   ± 6748.705  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     469705.006   ± 7260.392  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488208.256   ± 2501.386  ops/s
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
