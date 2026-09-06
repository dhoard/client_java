# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-06T08:00:48Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 61.44K | ± 3.86K | ops/s |
| prometheusNoLabelsInc | 56.69K | ± 462.64 | ops/s |
| prometheusAdd | 51.50K | ± 140.27 | ops/s |
| codahaleIncNoLabels | 44.00K | ± 7.66K | ops/s |
| openTelemetryIncNoLabels | 18.14K | ± 714.56 | ops/s |
| openTelemetryInc | 14.90K | ± 679.54 | ops/s |
| openTelemetryAdd | 12.95K | ± 51.95 | ops/s |
| simpleclientInc | 6.57K | ± 53.92 | ops/s |
| simpleclientAdd | 6.47K | ± 61.70 | ops/s |
| simpleclientNoLabelsInc | 6.33K | ± 6.09 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.33K | ± 85.77 | ops/s |
| prometheusClassic | 6.37K | ± 943.38 | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 21.02 | ops/s |
| simpleclient | 4.40K | ± 56.73 | ops/s |
| prometheusNative | 2.86K | ± 233.90 | ops/s |
| openTelemetryExponential | 881.21 | ± 122.00 | ops/s |
| openTelemetryClassic | 843.07 | ± 83.53 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.01K | ± 284.37 | ops/s |
| openMetricsWriteToNull | 23.81K | ± 35.43 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 497.65K | ± 7.27K | ops/s |
| prometheusWriteToByteArray | 490.69K | ± 11.27K | ops/s |
| openMetricsWriteToNull | 474.26K | ± 7.23K | ops/s |
| openMetricsWriteToByteArray | 471.22K | ± 8.17K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43995.886   ± 7655.290  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12951.734     ± 51.951  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14897.764    ± 679.543  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18143.881    ± 714.562  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51500.411    ± 140.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      61439.999   ± 3860.522  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56691.471    ± 462.639  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6467.614     ± 61.697  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6569.151     ± 53.924  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6334.732      ± 6.086  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        843.072     ± 83.532  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        881.214    ± 122.000  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6368.207    ± 943.378  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12325.654     ± 85.765  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4521.408     ± 21.017  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2861.148    ± 233.895  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4400.069     ± 56.734  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23808.742     ± 35.432  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24009.104    ± 284.375  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471224.387   ± 8172.804  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474256.844   ± 7231.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     490694.744  ± 11273.638  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497652.934   ± 7274.051  ops/s
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
