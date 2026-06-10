# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-10T07:29:24Z
- **Commit:** [`65d57b0`](https://github.com/dhoard/client_java/commit/65d57b020c6893283d5b4b85d76d86dfd7389cc8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.03K | ± 1.66K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.77K | ± 801.55 | ops/s | 1.1x slower |
| prometheusAdd | 48.93K | ± 613.27 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.59K | ± 1.63K | ops/s | 1.3x slower |
| simpleclientAdd | 6.14K | ± 88.39 | ops/s | 9.4x slower |
| simpleclientInc | 6.11K | ± 81.81 | ops/s | 9.5x slower |
| openTelemetryIncNoLabels | 6.01K | ± 1.35K | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.90K | ± 60.26 | ops/s | 9.8x slower |
| openTelemetryAdd | 5.26K | ± 159.53 | ops/s | 11x slower |
| openTelemetryInc | 4.77K | ± 858.85 | ops/s | 12x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 937.75 | ops/s | **fastest** |
| simpleclient | 4.18K | ± 11.66 | ops/s | 1.3x slower |
| prometheusNative | 3.06K | ± 106.96 | ops/s | 1.8x slower |
| openTelemetryClassic | 719.19 | ± 7.04 | ops/s | 7.6x slower |
| openTelemetryExponential | 559.05 | ± 12.43 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.32K | ± 202.63 | ops/s | **fastest** |
| prometheusWriteToNull | 27.19K | ± 321.88 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 575.04K | ± 5.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 569.55K | ± 4.57K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.13K | ± 3.81K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 530.78K | ± 5.73K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43585.887   ± 1631.613  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5262.873    ± 159.535  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4765.462    ± 858.846  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6009.025   ± 1351.327  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48925.977    ± 613.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58026.389   ± 1658.230  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51772.133    ± 801.552  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6140.673     ± 88.394  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6109.796     ± 81.815  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5897.963     ± 60.265  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        719.191      ± 7.042  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        559.049     ± 12.431  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5487.250    ± 937.746  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3060.180    ± 106.958  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4178.210     ± 11.664  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27315.582    ± 202.628  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27193.066    ± 321.876  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     530783.109   ± 5733.929  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543130.078   ± 3810.355  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     569554.201   ± 4567.304  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     575035.159   ± 5509.317  ops/s
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
