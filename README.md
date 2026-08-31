# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-31T09:12:51Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 76.53K | ± 530.80 | ops/s |
| prometheusNoLabelsInc | 65.74K | ± 59.06 | ops/s |
| prometheusAdd | 63.14K | ± 787.35 | ops/s |
| codahaleIncNoLabels | 55.87K | ± 2.08K | ops/s |
| openTelemetryIncNoLabels | 21.78K | ± 352.10 | ops/s |
| openTelemetryInc | 17.62K | ± 278.68 | ops/s |
| openTelemetryAdd | 15.30K | ± 671.41 | ops/s |
| simpleclientInc | 8.04K | ± 75.20 | ops/s |
| simpleclientNoLabelsInc | 7.80K | ± 250.59 | ops/s |
| simpleclientAdd | 7.58K | ± 354.93 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.66K | ± 187.64 | ops/s |
| prometheusClassicSingleThread | 7.48K | ± 38.71 | ops/s |
| simpleclient | 5.85K | ± 55.00 | ops/s |
| prometheusClassic | 5.67K | ± 718.32 | ops/s |
| prometheusNative | 3.91K | ± 389.48 | ops/s |
| openTelemetryClassic | 1.08K | ± 118.33 | ops/s |
| openTelemetryExponential | 816.15 | ± 12.54 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.35K | ± 208.68 | ops/s |
| openMetricsWriteToNull | 35.09K | ± 365.79 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 704.88K | ± 4.88K | ops/s |
| prometheusWriteToByteArray | 692.29K | ± 4.79K | ops/s |
| openMetricsWriteToNull | 658.91K | ± 4.61K | ops/s |
| openMetricsWriteToByteArray | 650.74K | ± 4.03K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55865.969   ± 2080.008  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15296.406    ± 671.414  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17621.440    ± 278.681  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21777.131    ± 352.101  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63139.716    ± 787.352  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76532.135    ± 530.798  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65742.880     ± 59.064  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7577.159    ± 354.927  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8040.304     ± 75.199  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7797.526    ± 250.595  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1079.993    ± 118.332  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        816.152     ± 12.536  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5672.598    ± 718.323  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17655.786    ± 187.641  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7483.812     ± 38.710  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3907.653    ± 389.481  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5854.960     ± 54.996  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35091.511    ± 365.792  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35345.923    ± 208.681  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     650740.737   ± 4026.991  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     658914.318   ± 4611.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     692289.996   ± 4788.267  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     704878.364   ± 4879.096  ops/s
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
