# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-03T05:34:29Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.13K | ± 1.12K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.43K | ± 1.10K | ops/s | 1.2x slower |
| prometheusAdd | 51.36K | ± 378.42 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.03K | ± 2.24K | ops/s | 1.4x slower |
| simpleclientInc | 6.67K | ± 77.08 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.48K | ± 207.18 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 240.62 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 196.71 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.28K | ± 109.02 | ops/s | 52x slower |
| openTelemetryAdd | 1.26K | ± 6.40 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.47K | ± 1.60K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 48.58 | ops/s | 1.2x slower |
| prometheusNative | 2.93K | ± 270.80 | ops/s | 1.9x slower |
| openTelemetryClassic | 735.92 | ± 60.00 | ops/s | 7.4x slower |
| openTelemetryExponential | 560.72 | ± 25.70 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 493.43K | ± 3.72K | ops/s | **fastest** |
| prometheusWriteToByteArray | 484.28K | ± 4.34K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.10K | ± 3.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.17K | ± 5.09K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48029.511   ± 2235.035  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1258.584      ± 6.402  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1355.312    ± 196.709  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1282.765    ± 109.020  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51363.108    ± 378.420  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66134.141   ± 1118.285  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56427.510   ± 1099.998  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6327.569    ± 240.620  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6667.660     ± 77.084  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6483.962    ± 207.180  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        735.925     ± 59.999  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        560.719     ± 25.697  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5472.513   ± 1596.195  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2927.164    ± 270.798  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.184     ± 48.581  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472172.834   ± 5092.994  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477095.720   ± 3496.873  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484283.324   ± 4340.380  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     493425.987   ± 3720.797  ops/s
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
