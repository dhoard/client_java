# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-09T08:15:06Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusNoLabelsInc | 26.38K | ± 502.91 | ops/s |
| prometheusInc | 26.37K | ± 325.22 | ops/s |
| codahaleIncNoLabels | 26.22K | ± 1.74K | ops/s |
| prometheusAdd | 25.74K | ± 384.27 | ops/s |
| openTelemetryIncNoLabels | 17.15K | ± 79.44 | ops/s |
| openTelemetryInc | 15.36K | ± 120.33 | ops/s |
| openTelemetryAdd | 13.37K | ± 118.38 | ops/s |
| simpleclientInc | 6.67K | ± 89.44 | ops/s |
| simpleclientNoLabelsInc | 6.65K | ± 47.59 | ops/s |
| simpleclientAdd | 6.36K | ± 182.75 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 6.84K | ± 92.52 | ops/s |
| simpleclient | 4.35K | ± 51.80 | ops/s |
| prometheusClassicSingleThread | 2.92K | ± 101.50 | ops/s |
| prometheusClassic | 2.45K | ± 371.17 | ops/s |
| prometheusNative | 2.06K | ± 308.99 | ops/s |
| openTelemetryClassic | 478.48 | ± 24.62 | ops/s |
| openTelemetryExponential | 468.55 | ± 9.75 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 18.04K | ± 146.37 | ops/s |
| openMetricsWriteToNull | 18.01K | ± 161.50 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 286.28K | ± 3.39K | ops/s |
| prometheusWriteToNull | 286.06K | ± 1.01K | ops/s |
| openMetricsWriteToByteArray | 270.67K | ± 2.07K | ops/s |
| openMetricsWriteToNull | 268.95K | ± 2.11K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      26215.051   ± 1736.607  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      13365.104    ± 118.382  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15362.769    ± 120.327  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17151.208     ± 79.441  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      25741.952    ± 384.267  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      26372.327    ± 325.221  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      26382.622    ± 502.915  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6361.615    ± 182.754  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6669.650     ± 89.438  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6653.954     ± 47.591  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        478.485     ± 24.616  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        468.554      ± 9.747  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2452.154    ± 371.173  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       6839.586     ± 92.516  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       2923.594    ± 101.500  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2057.897    ± 308.994  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4345.788     ± 51.797  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18013.909    ± 161.496  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18038.904    ± 146.375  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     270670.659   ± 2068.669  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     268947.814   ± 2107.987  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     286275.756   ± 3389.485  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     286056.607   ± 1006.098  ops/s
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
