# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-11T09:22:54Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.75K | ± 151.53 | ops/s |
| prometheusNoLabelsInc | 56.64K | ± 298.18 | ops/s |
| prometheusAdd | 50.38K | ± 286.74 | ops/s |
| codahaleIncNoLabels | 48.50K | ± 1.44K | ops/s |
| openTelemetryIncNoLabels | 18.47K | ± 87.53 | ops/s |
| openTelemetryInc | 15.18K | ± 293.12 | ops/s |
| openTelemetryAdd | 12.73K | ± 365.23 | ops/s |
| simpleclientInc | 6.55K | ± 62.05 | ops/s |
| simpleclientNoLabelsInc | 6.36K | ± 36.80 | ops/s |
| simpleclientAdd | 6.23K | ± 322.31 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.32K | ± 31.22 | ops/s |
| prometheusClassicSingleThread | 4.61K | ± 12.73 | ops/s |
| simpleclient | 4.48K | ± 47.98 | ops/s |
| prometheusClassic | 4.08K | ± 126.14 | ops/s |
| prometheusNative | 2.66K | ± 104.66 | ops/s |
| openTelemetryClassic | 837.13 | ± 73.05 | ops/s |
| openTelemetryExponential | 800.46 | ± 190.75 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.57K | ± 1.40K | ops/s |
| openMetricsWriteToNull | 23.29K | ± 614.92 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 499.96K | ± 2.77K | ops/s |
| prometheusWriteToByteArray | 495.91K | ± 2.67K | ops/s |
| openMetricsWriteToNull | 482.18K | ± 5.64K | ops/s |
| openMetricsWriteToByteArray | 478.05K | ± 3.78K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48497.352   ± 1443.239  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12726.492    ± 365.233  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15179.733    ± 293.121  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18466.783     ± 87.530  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50382.016    ± 286.737  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65749.403    ± 151.530  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56638.963    ± 298.180  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6231.194    ± 322.308  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6545.833     ± 62.046  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6360.897     ± 36.797  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        837.127     ± 73.049  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        800.455    ± 190.750  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4080.393    ± 126.139  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12322.064     ± 31.223  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4611.881     ± 12.729  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2659.351    ± 104.658  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4483.891     ± 47.980  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23286.750    ± 614.917  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23573.152   ± 1403.846  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     478045.695   ± 3779.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     482182.924   ± 5640.440  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495908.844   ± 2674.065  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     499957.838   ± 2765.390  ops/s
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
