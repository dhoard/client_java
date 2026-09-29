# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-29T09:01:46Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusNoLabelsInc | 30.17K | ± 384.15 | ops/s |
| prometheusInc | 29.88K | ± 376.03 | ops/s |
| prometheusAdd | 29.11K | ± 565.26 | ops/s |
| codahaleIncNoLabels | 28.86K | ± 1.10K | ops/s |
| openTelemetryIncNoLabels | 19.11K | ± 344.12 | ops/s |
| openTelemetryInc | 16.54K | ± 306.00 | ops/s |
| openTelemetryAdd | 14.11K | ± 211.88 | ops/s |
| simpleclientInc | 7.36K | ± 124.06 | ops/s |
| simpleclientAdd | 7.29K | ± 157.48 | ops/s |
| simpleclientNoLabelsInc | 7.14K | ± 206.40 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 7.21K | ± 192.21 | ops/s |
| simpleclient | 4.84K | ± 119.82 | ops/s |
| prometheusClassic | 3.73K | ± 2.14K | ops/s |
| prometheusClassicSingleThread | 3.28K | ± 120.23 | ops/s |
| prometheusNative | 2.43K | ± 167.49 | ops/s |
| openTelemetryClassic | 523.88 | ± 20.21 | ops/s |
| openTelemetryExponential | 498.82 | ± 65.08 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 20.22K | ± 337.87 | ops/s |
| prometheusWriteToNull | 19.98K | ± 306.04 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 341.99K | ± 10.34K | ops/s |
| prometheusWriteToNull | 336.08K | ± 17.08K | ops/s |
| openMetricsWriteToNull | 307.06K | ± 7.93K | ops/s |
| openMetricsWriteToByteArray | 303.81K | ± 6.62K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28861.091   ± 1098.923  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      14105.334    ± 211.880  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      16536.295    ± 306.004  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      19112.995    ± 344.124  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      29113.195    ± 565.259  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      29877.888    ± 376.033  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30166.691    ± 384.150  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7287.332    ± 157.483  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7358.197    ± 124.055  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7140.568    ± 206.404  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        523.882     ± 20.208  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        498.824     ± 65.077  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3729.685   ± 2143.248  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7209.194    ± 192.213  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3277.498    ± 120.227  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2431.249    ± 167.494  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4840.216    ± 119.817  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      20218.906    ± 337.868  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      19982.584    ± 306.040  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     303810.227   ± 6622.753  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     307062.802   ± 7934.179  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     341985.019  ± 10342.126  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     336076.801  ± 17077.498  ops/s
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
