# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-27T08:40:48Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 75.23K | ± 3.20K | ops/s |
| prometheusNoLabelsInc | 66.36K | ± 699.22 | ops/s |
| prometheusAdd | 62.26K | ± 450.55 | ops/s |
| codahaleIncNoLabels | 57.09K | ± 491.07 | ops/s |
| openTelemetryIncNoLabels | 22.11K | ± 25.69 | ops/s |
| openTelemetryInc | 17.41K | ± 45.52 | ops/s |
| openTelemetryAdd | 15.67K | ± 141.15 | ops/s |
| simpleclientInc | 8.00K | ± 129.28 | ops/s |
| simpleclientAdd | 7.70K | ± 385.14 | ops/s |
| simpleclientNoLabelsInc | 7.57K | ± 72.95 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.96K | ± 177.28 | ops/s |
| prometheusClassicSingleThread | 7.54K | ± 20.94 | ops/s |
| prometheusClassic | 7.06K | ± 2.45K | ops/s |
| simpleclient | 5.79K | ± 107.62 | ops/s |
| prometheusNative | 3.63K | ± 173.43 | ops/s |
| openTelemetryClassic | 1.10K | ± 100.03 | ops/s |
| openTelemetryExponential | 873.67 | ± 21.88 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.32K | ± 317.47 | ops/s |
| openMetricsWriteToNull | 34.98K | ± 242.10 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 710.29K | ± 3.12K | ops/s |
| prometheusWriteToByteArray | 693.22K | ± 6.07K | ops/s |
| openMetricsWriteToNull | 662.72K | ± 2.62K | ops/s |
| openMetricsWriteToByteArray | 647.02K | ± 4.69K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57087.830    ± 491.067  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15668.631    ± 141.148  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17411.418     ± 45.518  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22106.104     ± 25.686  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62257.199    ± 450.549  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75226.799   ± 3197.848  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66364.720    ± 699.222  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7700.765    ± 385.144  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8003.609    ± 129.282  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7565.918     ± 72.948  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1095.773    ± 100.027  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        873.669     ± 21.884  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7064.474   ± 2451.037  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17962.448    ± 177.280  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7537.991     ± 20.938  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3625.708    ± 173.432  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5786.678    ± 107.622  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34978.663    ± 242.098  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35324.633    ± 317.468  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     647023.907   ± 4691.095  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     662720.917   ± 2620.561  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     693217.782   ± 6073.195  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     710292.831   ± 3116.955  ops/s
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
