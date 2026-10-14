# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-14T08:15:02Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 66.92K | ± 610.18 | ops/s |
| prometheusNoLabelsInc | 64.29K | ± 601.86 | ops/s |
| codahaleIncNoLabels | 58.94K | ± 646.17 | ops/s |
| prometheusAdd | 55.12K | ± 371.30 | ops/s |
| openTelemetryIncNoLabels | 29.45K | ± 163.35 | ops/s |
| openTelemetryInc | 25.23K | ± 176.51 | ops/s |
| openTelemetryAdd | 21.82K | ± 291.45 | ops/s |
| simpleclientInc | 10.37K | ± 51.93 | ops/s |
| simpleclientNoLabelsInc | 10.35K | ± 271.27 | ops/s |
| simpleclientAdd | 10.12K | ± 60.87 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.11K | ± 327.25 | ops/s |
| prometheusClassic | 7.71K | ± 1.95K | ops/s |
| simpleclient | 7.05K | ± 192.96 | ops/s |
| prometheusNative | 4.80K | ± 608.46 | ops/s |
| prometheusClassicSingleThread | 4.45K | ± 125.04 | ops/s |
| openTelemetryClassic | 1.07K | ± 62.94 | ops/s |
| openTelemetryExponential | 925.01 | ± 42.77 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 33.99K | ± 283.39 | ops/s |
| prometheusWriteToNull | 32.95K | ± 4.24K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 723.22K | ± 20.93K | ops/s |
| prometheusWriteToByteArray | 710.76K | ± 48.15K | ops/s |
| openMetricsWriteToNull | 698.33K | ± 39.91K | ops/s |
| openMetricsWriteToByteArray | 630.81K | ± 65.49K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      58944.174    ± 646.168  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      21823.266    ± 291.446  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      25229.214    ± 176.514  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      29454.755    ± 163.349  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      55121.380    ± 371.296  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66924.355    ± 610.181  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64286.408    ± 601.865  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10120.157     ± 60.866  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10366.682     ± 51.925  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10349.754    ± 271.274  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1073.006     ± 62.939  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        925.008     ± 42.771  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7711.204   ± 1950.106  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15110.342    ± 327.254  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4447.363    ± 125.038  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4795.166    ± 608.464  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7045.369    ± 192.960  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      33993.094    ± 283.393  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      32948.312   ± 4241.788  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     630807.652  ± 65493.694  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     698329.623  ± 39913.153  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     710756.095  ± 48147.481  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     723224.068  ± 20934.724  ops/s
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
