# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-15T05:39:14Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.63K | ± 672.75 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.12K | ± 1.27K | ops/s | 1.2x slower |
| prometheusAdd | 51.62K | ± 172.73 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.22K | ± 976.62 | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 149.86 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.57K | ± 182.38 | ops/s | 10x slower |
| simpleclientAdd | 6.55K | ± 10.30 | ops/s | 10x slower |
| openTelemetryInc | 1.28K | ± 10.34 | ops/s | 52x slower |
| openTelemetryAdd | 1.26K | ± 82.12 | ops/s | 53x slower |
| openTelemetryIncNoLabels | 1.20K | ± 38.70 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.19K | ± 1.64K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 56.97 | ops/s | 1.1x slower |
| prometheusNative | 2.82K | ± 280.93 | ops/s | 1.8x slower |
| openTelemetryClassic | 693.39 | ± 14.48 | ops/s | 7.5x slower |
| openTelemetryExponential | 562.04 | ± 20.75 | ops/s | 9.2x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.24K | ± 1.69K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.67K | ± 2.29K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.54K | ± 2.15K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.70K | ± 3.87K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48217.149    ± 976.622  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1260.649     ± 82.125  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1275.004     ± 10.342  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1201.473     ± 38.703  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51622.939    ± 172.733  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66628.155    ± 672.749  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56119.562   ± 1266.012  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6554.369     ± 10.305  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6592.103    ± 149.863  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6565.764    ± 182.376  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        693.388     ± 14.478  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        562.042     ± 20.752  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5194.581   ± 1644.175  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2815.543    ± 280.930  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.029     ± 56.973  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479702.767   ± 3874.822  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483543.200   ± 2152.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488674.949   ± 2288.399  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493236.030   ± 1693.960  ops/s
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
