# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-11T08:09:57Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 65.26K | ± 1.50K | ops/s |
| prometheusNoLabelsInc | 56.52K | ± 358.03 | ops/s |
| prometheusAdd | 51.20K | ± 117.18 | ops/s |
| codahaleIncNoLabels | 47.36K | ± 469.82 | ops/s |
| openTelemetryIncNoLabels | 18.33K | ± 250.11 | ops/s |
| openTelemetryInc | 14.84K | ± 181.80 | ops/s |
| openTelemetryAdd | 12.86K | ± 94.12 | ops/s |
| simpleclientInc | 6.56K | ± 46.26 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 16.38 | ops/s |
| simpleclientAdd | 6.33K | ± 184.40 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.34K | ± 90.04 | ops/s |
| prometheusClassic | 6.26K | ± 2.91K | ops/s |
| prometheusClassicSingleThread | 4.61K | ± 28.62 | ops/s |
| simpleclient | 4.43K | ± 39.12 | ops/s |
| prometheusNative | 3.00K | ± 325.04 | ops/s |
| openTelemetryExponential | 832.28 | ± 125.63 | ops/s |
| openTelemetryClassic | 789.59 | ± 28.59 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.60K | ± 794.74 | ops/s |
| openMetricsWriteToNull | 23.36K | ± 997.42 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 505.57K | ± 10.88K | ops/s |
| prometheusWriteToByteArray | 498.34K | ± 8.50K | ops/s |
| openMetricsWriteToNull | 488.80K | ± 4.33K | ops/s |
| openMetricsWriteToByteArray | 483.16K | ± 6.16K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47357.104    ± 469.816  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12857.901     ± 94.120  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14840.524    ± 181.802  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18330.322    ± 250.107  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51197.107    ± 117.184  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65264.666   ± 1497.085  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56515.850    ± 358.029  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6333.022    ± 184.398  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6562.180     ± 46.256  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.158     ± 16.376  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        789.593     ± 28.592  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        832.279    ± 125.633  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6261.416   ± 2912.450  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12344.239     ± 90.037  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4605.531     ± 28.616  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2995.875    ± 325.038  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4425.586     ± 39.124  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23360.062    ± 997.418  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23596.768    ± 794.743  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483161.101   ± 6161.117  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488799.776   ± 4331.972  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     498336.166   ± 8502.772  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     505573.420  ± 10880.288  ops/s
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
