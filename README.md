# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-10T09:15:11Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| codahaleIncNoLabels | 27.50K | ± 116.34 | ops/s |
| prometheusNoLabelsInc | 26.53K | ± 113.15 | ops/s |
| prometheusInc | 26.32K | ± 205.77 | ops/s |
| prometheusAdd | 25.45K | ± 424.69 | ops/s |
| openTelemetryIncNoLabels | 16.83K | ± 179.19 | ops/s |
| openTelemetryInc | 15.25K | ± 116.07 | ops/s |
| openTelemetryAdd | 13.19K | ± 115.74 | ops/s |
| simpleclientInc | 6.72K | ± 35.00 | ops/s |
| simpleclientNoLabelsInc | 6.56K | ± 22.37 | ops/s |
| simpleclientAdd | 6.41K | ± 96.01 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 6.81K | ± 31.89 | ops/s |
| simpleclient | 4.29K | ± 11.12 | ops/s |
| prometheusClassicSingleThread | 2.91K | ± 85.39 | ops/s |
| prometheusClassic | 2.88K | ± 1.65K | ops/s |
| prometheusNative | 2.28K | ± 131.61 | ops/s |
| openTelemetryClassic | 490.28 | ± 99.33 | ops/s |
| openTelemetryExponential | 436.38 | ± 50.92 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 17.89K | ± 27.85 | ops/s |
| prometheusWriteToNull | 17.85K | ± 55.72 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 300.21K | ± 1.17K | ops/s |
| prometheusWriteToByteArray | 296.34K | ± 1.40K | ops/s |
| openMetricsWriteToNull | 278.86K | ± 1.84K | ops/s |
| openMetricsWriteToByteArray | 278.16K | ± 1.42K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      27501.195    ± 116.342  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13193.770    ± 115.744  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15250.914    ± 116.069  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16832.131    ± 179.188  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25454.229    ± 424.688  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26319.414    ± 205.765  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26533.629    ± 113.148  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6408.691     ± 96.005  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6721.749     ± 34.995  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6563.845     ± 22.369  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        490.281     ± 99.330  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        436.385     ± 50.923  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2881.191   ± 1652.469  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6811.990     ± 31.888  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2911.378     ± 85.390  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2284.869    ± 131.613  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4293.667     ± 11.120  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      17889.623     ± 27.855  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      17851.876     ± 55.722  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     278158.877   ± 1424.668  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     278859.964   ± 1837.553  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     296335.884   ± 1404.353  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     300207.046   ± 1174.516  ops/s
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
