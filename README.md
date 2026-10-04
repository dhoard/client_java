# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-04T08:56:50Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 77.29K | ± 143.92 | ops/s |
| prometheusNoLabelsInc | 64.71K | ± 3.28K | ops/s |
| prometheusAdd | 63.08K | ± 869.27 | ops/s |
| codahaleIncNoLabels | 57.49K | ± 393.93 | ops/s |
| openTelemetryIncNoLabels | 22.20K | ± 118.25 | ops/s |
| openTelemetryInc | 17.75K | ± 236.64 | ops/s |
| openTelemetryAdd | 15.67K | ± 58.05 | ops/s |
| simpleclientInc | 7.82K | ± 140.87 | ops/s |
| simpleclientNoLabelsInc | 7.61K | ± 36.75 | ops/s |
| simpleclientAdd | 7.59K | ± 173.54 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.49K | ± 163.42 | ops/s |
| prometheusClassic | 8.54K | ± 3.37K | ops/s |
| prometheusClassicSingleThread | 7.52K | ± 19.17 | ops/s |
| simpleclient | 5.63K | ± 288.84 | ops/s |
| prometheusNative | 4.04K | ± 75.57 | ops/s |
| openTelemetryClassic | 1.03K | ± 60.07 | ops/s |
| openTelemetryExponential | 870.91 | ± 56.91 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.31K | ± 381.69 | ops/s |
| openMetricsWriteToNull | 34.52K | ± 1.30K | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 700.07K | ± 5.96K | ops/s |
| prometheusWriteToByteArray | 681.70K | ± 2.06K | ops/s |
| openMetricsWriteToNull | 656.50K | ± 3.79K | ops/s |
| openMetricsWriteToByteArray | 643.17K | ± 2.96K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57493.054    ± 393.933  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15668.332     ± 58.053  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17748.308    ± 236.636  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22203.746    ± 118.250  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      63078.283    ± 869.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77288.300    ± 143.919  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64712.511   ± 3276.222  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7590.453    ± 173.536  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7821.637    ± 140.870  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7605.685     ± 36.753  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1031.704     ± 60.071  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        870.908     ± 56.905  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8535.615   ± 3369.415  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17489.837    ± 163.418  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7523.502     ± 19.172  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4038.664     ± 75.571  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5625.202    ± 288.837  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34522.313   ± 1296.263  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35305.844    ± 381.685  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     643174.195   ± 2963.194  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     656500.657   ± 3785.427  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     681703.735   ± 2055.678  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     700071.430   ± 5964.818  ops/s
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
