# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-09T09:31:16Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 76.93K | ± 470.50 | ops/s |
| prometheusNoLabelsInc | 66.69K | ± 45.06 | ops/s |
| prometheusAdd | 62.54K | ± 100.39 | ops/s |
| codahaleIncNoLabels | 56.90K | ± 168.82 | ops/s |
| openTelemetryIncNoLabels | 22.28K | ± 132.85 | ops/s |
| openTelemetryInc | 17.50K | ± 867.88 | ops/s |
| openTelemetryAdd | 15.69K | ± 46.56 | ops/s |
| simpleclientInc | 7.90K | ± 76.97 | ops/s |
| simpleclientNoLabelsInc | 7.66K | ± 15.11 | ops/s |
| simpleclientAdd | 7.48K | ± 356.79 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 18.08K | ± 74.58 | ops/s |
| prometheusClassic | 8.88K | ± 1.34K | ops/s |
| prometheusClassicSingleThread | 7.54K | ± 26.41 | ops/s |
| simpleclient | 5.88K | ± 55.04 | ops/s |
| prometheusNative | 4.18K | ± 75.43 | ops/s |
| openTelemetryClassic | 1.03K | ± 135.12 | ops/s |
| openTelemetryExponential | 875.06 | ± 31.14 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.64K | ± 115.90 | ops/s |
| openMetricsWriteToNull | 35.07K | ± 587.98 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 698.10K | ± 4.80K | ops/s |
| prometheusWriteToByteArray | 683.65K | ± 4.10K | ops/s |
| openMetricsWriteToNull | 659.15K | ± 4.11K | ops/s |
| openMetricsWriteToByteArray | 649.49K | ± 3.35K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56902.869    ± 168.822  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15693.970     ± 46.556  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17497.347    ± 867.880  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22282.238    ± 132.854  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62535.244    ± 100.393  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76934.891    ± 470.498  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66693.380     ± 45.057  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7479.478    ± 356.786  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7904.968     ± 76.970  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7656.425     ± 15.108  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1025.582    ± 135.117  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        875.063     ± 31.138  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8884.042   ± 1341.289  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18080.056     ± 74.580  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7538.594     ± 26.413  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4184.413     ± 75.433  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5879.325     ± 55.036  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35067.512    ± 587.983  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35638.044    ± 115.905  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     649489.238   ± 3349.063  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     659149.425   ± 4105.899  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     683652.270   ± 4101.666  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     698101.286   ± 4797.021  ops/s
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
