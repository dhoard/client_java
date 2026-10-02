# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T09:04:34Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 63.72K | ± 1.52K | ops/s |
| prometheusNoLabelsInc | 56.66K | ± 477.19 | ops/s |
| prometheusAdd | 51.46K | ± 229.48 | ops/s |
| codahaleIncNoLabels | 48.10K | ± 1.72K | ops/s |
| openTelemetryIncNoLabels | 18.52K | ± 105.98 | ops/s |
| openTelemetryInc | 14.97K | ± 364.76 | ops/s |
| openTelemetryAdd | 12.97K | ± 74.72 | ops/s |
| simpleclientInc | 6.56K | ± 124.78 | ops/s |
| simpleclientNoLabelsInc | 6.38K | ± 35.77 | ops/s |
| simpleclientAdd | 6.23K | ± 358.96 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.29K | ± 24.69 | ops/s |
| prometheusClassic | 6.06K | ± 1.49K | ops/s |
| prometheusClassicSingleThread | 4.59K | ± 31.50 | ops/s |
| simpleclient | 4.41K | ± 20.06 | ops/s |
| prometheusNative | 2.58K | ± 132.23 | ops/s |
| openTelemetryExponential | 943.72 | ± 77.14 | ops/s |
| openTelemetryClassic | 821.90 | ± 80.51 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.54K | ± 1.26K | ops/s |
| openMetricsWriteToNull | 22.72K | ± 554.54 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 505.31K | ± 3.73K | ops/s |
| prometheusWriteToByteArray | 500.64K | ± 7.30K | ops/s |
| openMetricsWriteToNull | 485.13K | ± 7.88K | ops/s |
| openMetricsWriteToByteArray | 482.48K | ± 4.42K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48099.031   ± 1722.074  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12970.788     ± 74.721  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14966.011    ± 364.762  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18519.208    ± 105.981  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51464.958    ± 229.480  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63723.056   ± 1521.647  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56656.742    ± 477.189  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6229.093    ± 358.959  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.639    ± 124.783  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6379.662     ± 35.766  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        821.903     ± 80.511  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        943.724     ± 77.139  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6061.067   ± 1490.196  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12290.118     ± 24.690  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4590.853     ± 31.497  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2577.322    ± 132.234  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4410.744     ± 20.064  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22719.925    ± 554.540  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23539.574   ± 1260.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482478.958   ± 4415.591  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485131.360   ± 7876.819  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     500641.904   ± 7298.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     505305.456   ± 3732.640  ops/s
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
