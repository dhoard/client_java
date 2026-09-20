# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T08:37:39Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.48K | ± 655.90 | ops/s |
| prometheusNoLabelsInc | 56.78K | ± 283.65 | ops/s |
| prometheusAdd | 51.22K | ± 371.52 | ops/s |
| codahaleIncNoLabels | 48.92K | ± 1.96K | ops/s |
| openTelemetryIncNoLabels | 18.54K | ± 64.53 | ops/s |
| openTelemetryInc | 14.96K | ± 197.46 | ops/s |
| openTelemetryAdd | 12.71K | ± 263.92 | ops/s |
| simpleclientInc | 6.58K | ± 10.89 | ops/s |
| simpleclientAdd | 6.42K | ± 90.95 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 28.77 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.26K | ± 38.21 | ops/s |
| prometheusClassic | 5.53K | ± 1.91K | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 56.82 | ops/s |
| simpleclient | 4.41K | ± 25.30 | ops/s |
| prometheusNative | 3.06K | ± 245.26 | ops/s |
| openTelemetryClassic | 843.94 | ± 68.10 | ops/s |
| openTelemetryExponential | 776.48 | ± 157.65 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.79K | ± 382.54 | ops/s |
| openMetricsWriteToNull | 23.56K | ± 606.10 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 494.67K | ± 10.33K | ops/s |
| prometheusWriteToByteArray | 493.15K | ± 4.93K | ops/s |
| openMetricsWriteToNull | 477.66K | ± 8.37K | ops/s |
| openMetricsWriteToByteArray | 473.62K | ± 3.21K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48918.611   ± 1958.385  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12706.377    ± 263.916  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14961.077    ± 197.463  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18541.384     ± 64.527  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51215.967    ± 371.518  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66480.612    ± 655.904  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56783.660    ± 283.647  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6424.353     ± 90.946  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.041     ± 10.885  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6353.722     ± 28.770  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        843.943     ± 68.105  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        776.484    ± 157.648  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5527.931   ± 1910.903  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12258.878     ± 38.205  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4549.181     ± 56.817  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3060.646    ± 245.260  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4412.164     ± 25.297  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23563.481    ± 606.101  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23792.220    ± 382.543  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473623.796   ± 3206.333  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477656.756   ± 8369.820  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493148.270   ± 4934.551  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494666.399  ± 10332.599  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
