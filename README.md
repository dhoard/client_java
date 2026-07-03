# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-03T06:58:10Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.78K | ± 1.62K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 292.73 | ops/s | 1.1x slower |
| prometheusAdd | 50.94K | ± 538.32 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.65K | ± 1.37K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 82.29 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.44K | ± 155.20 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 196.52 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.54K | ± 256.36 | ops/s | 18x slower |
| openTelemetryInc | 3.17K | ± 416.54 | ops/s | 20x slower |
| openTelemetryAdd | 3.08K | ± 65.51 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.71K | ± 1.03K | ops/s | **fastest** |
| simpleclient | 4.45K | ± 52.54 | ops/s | 1.3x slower |
| prometheusNative | 3.11K | ± 63.63 | ops/s | 1.8x slower |
| openTelemetryClassic | 757.51 | ± 32.38 | ops/s | 7.5x slower |
| openTelemetryExponential | 569.44 | ± 38.09 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.27K | ± 497.81 | ops/s | **fastest** |
| prometheusWriteToNull | 23.36K | ± 1.08K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 501.79K | ± 6.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.50K | ± 6.82K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 486.96K | ± 3.63K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.93K | ± 3.02K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47646.289   ± 1373.307  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3084.705     ± 65.513  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3167.303    ± 416.543  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3538.560    ± 256.363  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50944.077    ± 538.316  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64784.560   ± 1617.849  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56782.155    ± 292.734  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6335.285    ± 196.525  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.624     ± 82.294  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6438.020    ± 155.205  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        757.506     ± 32.377  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.445     ± 38.086  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5707.160   ± 1027.652  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3114.167     ± 63.626  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4448.414     ± 52.535  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24269.424    ± 497.809  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23362.727   ± 1083.737  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481927.368   ± 3016.200  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     486956.412   ± 3629.898  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499501.635   ± 6820.342  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501793.647   ± 6682.269  ops/s
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
