# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-18T08:13:25Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.87K | ± 1.23K | ops/s |
| prometheusNoLabelsInc | 55.94K | ± 615.03 | ops/s |
| prometheusAdd | 48.30K | ± 4.80K | ops/s |
| codahaleIncNoLabels | 48.06K | ± 1.74K | ops/s |
| openTelemetryIncNoLabels | 18.54K | ± 49.99 | ops/s |
| openTelemetryInc | 15.23K | ± 263.62 | ops/s |
| openTelemetryAdd | 12.89K | ± 141.90 | ops/s |
| simpleclientInc | 6.58K | ± 85.45 | ops/s |
| simpleclientAdd | 6.45K | ± 76.70 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 34.61 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.28K | ± 31.05 | ops/s |
| prometheusClassic | 6.47K | ± 1.20K | ops/s |
| prometheusClassicSingleThread | 4.57K | ± 26.75 | ops/s |
| simpleclient | 4.42K | ± 60.52 | ops/s |
| prometheusNative | 2.93K | ± 234.22 | ops/s |
| openTelemetryExponential | 847.88 | ± 143.93 | ops/s |
| openTelemetryClassic | 843.38 | ± 98.90 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.37K | ± 408.11 | ops/s |
| openMetricsWriteToNull | 23.01K | ± 1.10K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 494.72K | ± 3.65K | ops/s |
| prometheusWriteToByteArray | 485.22K | ± 2.05K | ops/s |
| openMetricsWriteToNull | 469.74K | ± 5.98K | ops/s |
| openMetricsWriteToByteArray | 464.46K | ± 4.93K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48060.666   ± 1742.731  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12888.687    ± 141.896  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15227.682    ± 263.616  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18539.163     ± 49.987  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48303.869   ± 4795.085  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64866.523   ± 1231.841  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55938.373    ± 615.031  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6452.793     ± 76.702  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6583.138     ± 85.453  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6352.335     ± 34.606  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        843.375     ± 98.898  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        847.880    ± 143.927  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6466.276   ± 1195.646  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12277.702     ± 31.045  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4572.712     ± 26.752  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2926.972    ± 234.224  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4415.636     ± 60.521  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23013.351   ± 1102.763  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23369.846    ± 408.111  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464460.556   ± 4934.383  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     469739.470   ± 5977.919  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485219.110   ± 2045.786  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494721.135   ± 3646.043  ops/s
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
