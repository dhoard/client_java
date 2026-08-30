# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-30T09:01:41Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 57.83K | ± 3.92K | ops/s |
| prometheusNoLabelsInc | 51.86K | ± 111.69 | ops/s |
| prometheusAdd | 48.51K | ± 42.54 | ops/s |
| codahaleIncNoLabels | 43.95K | ± 441.39 | ops/s |
| openTelemetryIncNoLabels | 17.08K | ± 38.86 | ops/s |
| openTelemetryInc | 13.54K | ± 29.26 | ops/s |
| openTelemetryAdd | 12.09K | ± 225.24 | ops/s |
| simpleclientAdd | 6.10K | ± 80.80 | ops/s |
| simpleclientInc | 6.07K | ± 27.19 | ops/s |
| simpleclientNoLabelsInc | 5.92K | ± 22.23 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 13.68K | ± 123.36 | ops/s |
| prometheusClassic | 6.97K | ± 1.62K | ops/s |
| prometheusClassicSingleThread | 5.81K | ± 13.07 | ops/s |
| simpleclient | 4.54K | ± 59.84 | ops/s |
| prometheusNative | 2.91K | ± 217.62 | ops/s |
| openTelemetryClassic | 822.45 | ± 24.71 | ops/s |
| openTelemetryExponential | 721.15 | ± 49.89 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.45K | ± 262.81 | ops/s |
| openMetricsWriteToNull | 27.44K | ± 97.25 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 581.87K | ± 4.23K | ops/s |
| prometheusWriteToByteArray | 574.03K | ± 5.54K | ops/s |
| openMetricsWriteToNull | 548.77K | ± 2.22K | ops/s |
| openMetricsWriteToByteArray | 536.01K | ± 3.61K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43949.462    ± 441.393  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12092.071    ± 225.238  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13542.392     ± 29.262  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17084.469     ± 38.861  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48507.322     ± 42.539  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57834.682   ± 3922.584  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51858.332    ± 111.688  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6099.756     ± 80.803  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6067.363     ± 27.192  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5922.932     ± 22.228  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        822.453     ± 24.712  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        721.152     ± 49.885  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6968.934   ± 1617.659  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13678.606    ± 123.358  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5811.337     ± 13.073  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2912.826    ± 217.623  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4541.034     ± 59.842  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27437.905     ± 97.255  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27445.637    ± 262.806  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536009.981   ± 3610.655  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     548773.898   ± 2219.302  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     574033.040   ± 5538.975  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581869.863   ± 4227.690  ops/s
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
