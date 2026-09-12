# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-12T08:02:57Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 64.54K | ± 2.89K | ops/s |
| prometheusNoLabelsInc | 56.83K | ± 357.75 | ops/s |
| prometheusAdd | 51.02K | ± 301.84 | ops/s |
| codahaleIncNoLabels | 45.81K | ± 6.30K | ops/s |
| openTelemetryIncNoLabels | 18.45K | ± 151.22 | ops/s |
| openTelemetryInc | 15.52K | ± 48.62 | ops/s |
| openTelemetryAdd | 12.96K | ± 84.72 | ops/s |
| simpleclientInc | 6.58K | ± 14.78 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 9.96 | ops/s |
| simpleclientAdd | 6.18K | ± 343.97 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.30K | ± 19.51 | ops/s |
| prometheusClassic | 5.58K | ± 1.34K | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 23.63 | ops/s |
| simpleclient | 4.28K | ± 125.25 | ops/s |
| prometheusNative | 2.84K | ± 240.85 | ops/s |
| openTelemetryExponential | 902.06 | ± 67.06 | ops/s |
| openTelemetryClassic | 830.40 | ± 21.05 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.51K | ± 857.05 | ops/s |
| openMetricsWriteToNull | 23.43K | ± 786.58 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 509.46K | ± 4.49K | ops/s |
| prometheusWriteToByteArray | 491.98K | ± 4.35K | ops/s |
| openMetricsWriteToNull | 484.58K | ± 4.17K | ops/s |
| openMetricsWriteToByteArray | 481.15K | ± 5.50K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45814.375   ± 6297.698  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12961.228     ± 84.724  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15516.099     ± 48.624  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18453.610    ± 151.222  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51015.709    ± 301.838  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64541.563   ± 2893.027  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56833.950    ± 357.747  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6183.089    ± 343.971  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.424     ± 14.781  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.858      ± 9.961  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        830.395     ± 21.054  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        902.058     ± 67.060  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5578.149   ± 1341.632  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12302.682     ± 19.506  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4550.934     ± 23.634  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2839.039    ± 240.849  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4284.984    ± 125.247  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23427.307    ± 786.584  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23514.024    ± 857.046  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481152.914   ± 5503.249  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     484582.606   ± 4171.568  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491980.756   ± 4345.339  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509458.050   ± 4486.758  ops/s
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
