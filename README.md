# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-06T07:02:37Z
- **Commit:** [`574fb73`](https://github.com/dhoard/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 76.16K | ± 1.89K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.14K | ± 693.69 | ops/s | 1.2x slower |
| prometheusAdd | 62.58K | ± 33.61 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.78K | ± 173.17 | ops/s | 1.3x slower |
| simpleclientInc | 7.90K | ± 80.06 | ops/s | 9.6x slower |
| simpleclientAdd | 7.72K | ± 326.27 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 7.60K | ± 7.33 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 7.11K | ± 1.02K | ops/s | 11x slower |
| openTelemetryInc | 6.52K | ± 1.45K | ops/s | 12x slower |
| openTelemetryAdd | 5.51K | ± 1.06K | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.48K | ± 3.40K | ops/s | **fastest** |
| simpleclient | 5.42K | ± 40.23 | ops/s | 1.4x slower |
| prometheusNative | 3.58K | ± 379.41 | ops/s | 2.1x slower |
| openTelemetryClassic | 880.25 | ± 8.06 | ops/s | 8.5x slower |
| openTelemetryExponential | 699.19 | ± 4.83 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 35.56K | ± 133.97 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.66K | ± 602.34 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 706.10K | ± 10.10K | ops/s | **fastest** |
| prometheusWriteToByteArray | 686.90K | ± 4.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 659.65K | ± 6.12K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 641.69K | ± 5.24K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56783.930    ± 173.169  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5511.965   ± 1062.807  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       6523.816   ± 1447.201  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7111.914   ± 1023.946  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62579.725     ± 33.613  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76162.619   ± 1892.241  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66143.594    ± 693.689  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7716.435    ± 326.274  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7898.455     ± 80.061  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7598.288      ± 7.328  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        880.246      ± 8.057  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        699.191      ± 4.833  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7481.676   ± 3395.634  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3575.627    ± 379.408  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5421.905     ± 40.233  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34656.958    ± 602.341  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35560.383    ± 133.967  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     641685.501   ± 5238.097  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     659648.279   ± 6115.040  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     686896.178   ± 4259.361  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     706101.608  ± 10098.709  ops/s
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
