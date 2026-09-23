# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-23T08:17:24Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.13K | ± 749.20 | ops/s |
| prometheusNoLabelsInc | 55.70K | ± 1.12K | ops/s |
| prometheusAdd | 51.32K | ± 77.85 | ops/s |
| codahaleIncNoLabels | 42.86K | ± 6.76K | ops/s |
| openTelemetryIncNoLabels | 18.39K | ± 102.93 | ops/s |
| openTelemetryInc | 15.18K | ± 279.91 | ops/s |
| openTelemetryAdd | 12.91K | ± 43.56 | ops/s |
| simpleclientInc | 6.58K | ± 6.53 | ops/s |
| simpleclientAdd | 6.45K | ± 33.23 | ops/s |
| simpleclientNoLabelsInc | 6.37K | ± 33.01 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 17.63 | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 42.56 | ops/s |
| simpleclient | 4.46K | ± 47.56 | ops/s |
| prometheusClassic | 4.44K | ± 664.57 | ops/s |
| prometheusNative | 2.65K | ± 102.12 | ops/s |
| openTelemetryExponential | 831.14 | ± 140.11 | ops/s |
| openTelemetryClassic | 784.64 | ± 42.90 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.26K | ± 351.00 | ops/s |
| prometheusWriteToNull | 22.71K | ± 791.14 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 491.54K | ± 3.21K | ops/s |
| prometheusWriteToNull | 490.31K | ± 5.44K | ops/s |
| openMetricsWriteToNull | 465.39K | ± 9.58K | ops/s |
| openMetricsWriteToByteArray | 458.78K | ± 4.65K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42861.407   ± 6758.553  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12905.888     ± 43.559  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15181.082    ± 279.914  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18385.491    ± 102.932  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51315.951     ± 77.850  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64128.437    ± 749.196  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55697.163   ± 1115.204  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6451.632     ± 33.228  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.246      ± 6.534  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6365.082     ± 33.010  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        784.636     ± 42.898  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        831.139    ± 140.113  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4444.491    ± 664.572  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12302.714     ± 17.631  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4551.673     ± 42.556  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2652.947    ± 102.118  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.890     ± 47.559  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23261.493    ± 351.004  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      22713.952    ± 791.136  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458783.909   ± 4648.751  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     465387.318   ± 9576.677  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491536.214   ± 3213.873  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490313.281   ± 5440.192  ops/s
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
