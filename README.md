# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T08:18:48Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 58.27K | ± 3.85K | ops/s |
| prometheusNoLabelsInc | 50.93K | ± 2.04K | ops/s |
| prometheusAdd | 48.29K | ± 283.36 | ops/s |
| codahaleIncNoLabels | 44.78K | ± 533.17 | ops/s |
| openTelemetryIncNoLabels | 17.25K | ± 112.66 | ops/s |
| openTelemetryInc | 13.54K | ± 24.24 | ops/s |
| openTelemetryAdd | 12.09K | ± 213.57 | ops/s |
| simpleclientInc | 6.08K | ± 38.14 | ops/s |
| simpleclientAdd | 6.08K | ± 7.68 | ops/s |
| simpleclientNoLabelsInc | 5.89K | ± 9.83 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 13.96K | ± 37.45 | ops/s |
| prometheusClassicSingleThread | 5.84K | ± 15.89 | ops/s |
| prometheusClassic | 4.78K | ± 482.75 | ops/s |
| simpleclient | 4.54K | ± 83.39 | ops/s |
| prometheusNative | 3.07K | ± 172.22 | ops/s |
| openTelemetryClassic | 816.31 | ± 37.33 | ops/s |
| openTelemetryExponential | 690.41 | ± 30.67 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.62K | ± 417.61 | ops/s |
| openMetricsWriteToNull | 27.51K | ± 289.04 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 581.24K | ± 3.25K | ops/s |
| prometheusWriteToByteArray | 571.16K | ± 11.26K | ops/s |
| openMetricsWriteToNull | 548.55K | ± 5.01K | ops/s |
| openMetricsWriteToByteArray | 537.25K | ± 4.86K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44780.468    ± 533.167  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12094.963    ± 213.568  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13536.749     ± 24.243  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17245.950    ± 112.657  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48287.488    ± 283.364  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58267.371   ± 3846.403  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50928.389   ± 2038.241  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6076.124      ± 7.682  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6076.257     ± 38.135  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5887.678      ± 9.833  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        816.312     ± 37.326  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        690.415     ± 30.668  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4784.620    ± 482.750  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13957.767     ± 37.452  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5840.900     ± 15.892  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3069.276    ± 172.217  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4542.387     ± 83.389  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27506.162    ± 289.043  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27621.124    ± 417.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     537248.926   ± 4863.022  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548547.788   ± 5005.173  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     571158.764  ± 11259.923  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581238.865   ± 3252.192  ops/s
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
