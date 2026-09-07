# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-07T08:08:46Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.40K | ± 1.13K | ops/s |
| prometheusNoLabelsInc | 56.77K | ± 345.14 | ops/s |
| prometheusAdd | 51.55K | ± 186.34 | ops/s |
| codahaleIncNoLabels | 49.27K | ± 1.83K | ops/s |
| openTelemetryIncNoLabels | 18.51K | ± 51.67 | ops/s |
| openTelemetryInc | 14.65K | ± 86.33 | ops/s |
| openTelemetryAdd | 12.89K | ± 37.52 | ops/s |
| simpleclientInc | 6.66K | ± 58.55 | ops/s |
| simpleclientNoLabelsInc | 6.43K | ± 128.97 | ops/s |
| simpleclientAdd | 6.32K | ± 183.52 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.29K | ± 24.23 | ops/s |
| prometheusClassic | 7.15K | ± 2.14K | ops/s |
| prometheusClassicSingleThread | 4.53K | ± 23.40 | ops/s |
| simpleclient | 4.46K | ± 78.74 | ops/s |
| prometheusNative | 3.00K | ± 221.44 | ops/s |
| openTelemetryExponential | 838.74 | ± 138.50 | ops/s |
| openTelemetryClassic | 810.16 | ± 56.37 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.03K | ± 376.43 | ops/s |
| openMetricsWriteToNull | 23.68K | ± 625.64 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 504.69K | ± 7.25K | ops/s |
| prometheusWriteToByteArray | 498.51K | ± 5.05K | ops/s |
| openMetricsWriteToNull | 489.38K | ± 2.48K | ops/s |
| openMetricsWriteToByteArray | 482.31K | ± 4.45K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49267.005   ± 1828.709  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12888.956     ± 37.524  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14653.805     ± 86.329  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18513.865     ± 51.671  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51547.460    ± 186.339  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65397.711   ± 1132.695  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56773.077    ± 345.139  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6320.260    ± 183.518  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6662.486     ± 58.548  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6428.641    ± 128.966  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        810.160     ± 56.367  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        838.739    ± 138.503  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7148.109   ± 2141.817  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12287.342     ± 24.228  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4533.221     ± 23.399  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2999.403    ± 221.438  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4455.096     ± 78.740  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23681.019    ± 625.636  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24030.401    ± 376.430  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482311.429   ± 4449.165  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489378.667   ± 2475.221  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498507.661   ± 5053.868  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504688.167   ± 7251.438  ops/s
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
