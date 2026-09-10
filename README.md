# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-10T08:10:30Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 76.77K | ± 900.59 | ops/s |
| prometheusNoLabelsInc | 66.51K | ± 588.48 | ops/s |
| prometheusAdd | 63.06K | ± 843.78 | ops/s |
| codahaleIncNoLabels | 47.18K | ± 15.87K | ops/s |
| openTelemetryIncNoLabels | 22.09K | ± 242.57 | ops/s |
| openTelemetryInc | 17.74K | ± 165.23 | ops/s |
| openTelemetryAdd | 15.70K | ± 11.96 | ops/s |
| simpleclientInc | 7.99K | ± 107.67 | ops/s |
| simpleclientAdd | 7.93K | ± 70.86 | ops/s |
| simpleclientNoLabelsInc | 7.53K | ± 101.29 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 18.03K | ± 159.03 | ops/s |
| prometheusClassicSingleThread | 7.55K | ± 16.36 | ops/s |
| prometheusClassic | 6.71K | ± 1.31K | ops/s |
| simpleclient | 5.85K | ± 71.21 | ops/s |
| prometheusNative | 4.08K | ± 80.61 | ops/s |
| openTelemetryClassic | 1.04K | ± 50.84 | ops/s |
| openTelemetryExponential | 880.06 | ± 71.44 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 35.37K | ± 261.73 | ops/s |
| prometheusWriteToNull | 35.37K | ± 182.19 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 694.61K | ± 4.27K | ops/s |
| prometheusWriteToByteArray | 677.67K | ± 5.32K | ops/s |
| openMetricsWriteToNull | 651.49K | ± 4.55K | ops/s |
| openMetricsWriteToByteArray | 631.43K | ± 15.48K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47176.761  ± 15865.581  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15700.334     ± 11.961  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17738.961    ± 165.231  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22091.561    ± 242.568  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63063.383    ± 843.775  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76774.128    ± 900.587  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66512.386    ± 588.476  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7934.185     ± 70.859  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7992.503    ± 107.665  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7528.824    ± 101.288  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1042.277     ± 50.839  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        880.056     ± 71.439  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6714.889   ± 1307.783  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18032.953    ± 159.030  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7546.059     ± 16.363  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4083.995     ± 80.611  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5853.855     ± 71.206  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35373.273    ± 261.726  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35368.920    ± 182.189  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     631431.142  ± 15482.377  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     651494.085   ± 4548.688  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     677670.626   ± 5322.776  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     694605.875   ± 4265.928  ops/s
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
