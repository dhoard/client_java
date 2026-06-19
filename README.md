# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-19T08:12:00Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.64K | ± 598.74 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.09K | ± 489.49 | ops/s | 1.1x slower |
| prometheusAdd | 48.51K | ± 193.39 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.30K | ± 561.05 | ops/s | 1.3x slower |
| simpleclientInc | 6.14K | ± 68.05 | ops/s | 9.7x slower |
| simpleclientAdd | 6.01K | ± 154.57 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.93K | ± 74.50 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.39K | ± 444.65 | ops/s | 14x slower |
| openTelemetryInc | 4.11K | ± 360.54 | ops/s | 14x slower |
| openTelemetryAdd | 3.40K | ± 197.81 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.94K | ± 731.92 | ops/s | **fastest** |
| simpleclient | 4.50K | ± 136.14 | ops/s | 1.5x slower |
| prometheusNative | 3.10K | ± 181.44 | ops/s | 2.2x slower |
| openTelemetryClassic | 722.01 | ± 31.78 | ops/s | 9.6x slower |
| openTelemetryExponential | 539.08 | ± 26.08 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.54K | ± 209.10 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.34K | ± 278.39 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 565.79K | ± 5.24K | ops/s | **fastest** |
| prometheusWriteToByteArray | 559.29K | ± 2.36K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 532.62K | ± 3.17K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 519.84K | ± 3.83K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44304.697    ± 561.050  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3400.748    ± 197.808  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4113.925    ± 360.542  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4393.385    ± 444.649  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48513.521    ± 193.395  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59636.549    ± 598.739  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52092.352    ± 489.493  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6014.717    ± 154.575  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6136.440     ± 68.051  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5933.808     ± 74.504  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        722.011     ± 31.779  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.081     ± 26.081  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6943.801    ± 731.924  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3097.082    ± 181.440  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4500.385    ± 136.139  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27335.685    ± 278.386  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27539.829    ± 209.096  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519844.828   ± 3833.465  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     532618.879   ± 3166.508  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     559287.822   ± 2360.183  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     565790.297   ± 5243.340  ops/s
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
