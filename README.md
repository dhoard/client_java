# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-08T08:04:08Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.52K | ± 1.39K | ops/s |
| prometheusNoLabelsInc | 55.27K | ± 2.25K | ops/s |
| prometheusAdd | 51.36K | ± 147.37 | ops/s |
| codahaleIncNoLabels | 47.29K | ± 434.21 | ops/s |
| openTelemetryIncNoLabels | 18.11K | ± 423.21 | ops/s |
| openTelemetryInc | 15.03K | ± 405.70 | ops/s |
| openTelemetryAdd | 12.90K | ± 68.85 | ops/s |
| simpleclientInc | 6.58K | ± 9.94 | ops/s |
| simpleclientNoLabelsInc | 6.43K | ± 148.12 | ops/s |
| simpleclientAdd | 6.15K | ± 204.47 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 19.14 | ops/s |
| prometheusClassic | 7.03K | ± 221.94 | ops/s |
| prometheusClassicSingleThread | 4.58K | ± 33.22 | ops/s |
| simpleclient | 4.42K | ± 50.56 | ops/s |
| prometheusNative | 2.89K | ± 305.77 | ops/s |
| openTelemetryExponential | 848.54 | ± 68.04 | ops/s |
| openTelemetryClassic | 785.72 | ± 41.23 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.84K | ± 387.03 | ops/s |
| openMetricsWriteToNull | 23.12K | ± 321.51 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 496.12K | ± 4.80K | ops/s |
| prometheusWriteToByteArray | 495.11K | ± 3.48K | ops/s |
| openMetricsWriteToNull | 484.53K | ± 5.14K | ops/s |
| openMetricsWriteToByteArray | 469.61K | ± 13.12K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47291.463    ± 434.214  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12904.259     ± 68.852  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15028.662    ± 405.700  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18111.218    ± 423.207  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51355.875    ± 147.370  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65516.909   ± 1387.008  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55271.014   ± 2246.620  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6150.962    ± 204.473  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6579.870      ± 9.944  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6426.959    ± 148.115  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        785.718     ± 41.231  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        848.541     ± 68.039  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7029.134    ± 221.936  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12295.393     ± 19.141  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4583.437     ± 33.221  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2887.640    ± 305.772  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4424.690     ± 50.560  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23122.066    ± 321.505  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23838.148    ± 387.032  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469612.886  ± 13122.010  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484526.550   ± 5141.825  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495105.646   ± 3483.834  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496120.792   ± 4799.269  ops/s
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
