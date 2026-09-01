# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-01T08:19:15Z
- **Commit:** [`e43f451`](https://github.com/dhoard/client_java/commit/e43f4517810e3763fe863e2b84b55742b76df4c3)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 59.12K | ± 778.55 | ops/s |
| prometheusNoLabelsInc | 51.50K | ± 420.31 | ops/s |
| prometheusAdd | 48.71K | ± 942.87 | ops/s |
| codahaleIncNoLabels | 43.25K | ± 1.26K | ops/s |
| openTelemetryIncNoLabels | 14.75K | ± 3.74K | ops/s |
| openTelemetryInc | 14.13K | ± 323.05 | ops/s |
| openTelemetryAdd | 12.21K | ± 48.70 | ops/s |
| simpleclientInc | 6.08K | ± 124.73 | ops/s |
| simpleclientAdd | 6.00K | ± 207.44 | ops/s |
| simpleclientNoLabelsInc | 5.91K | ± 21.67 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.05K | ± 44.65 | ops/s |
| prometheusClassic | 7.02K | ± 578.26 | ops/s |
| prometheusClassicSingleThread | 5.82K | ± 12.66 | ops/s |
| simpleclient | 4.52K | ± 134.36 | ops/s |
| prometheusNative | 3.00K | ± 276.96 | ops/s |
| openTelemetryClassic | 845.14 | ± 77.04 | ops/s |
| openTelemetryExponential | 678.08 | ± 10.03 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 27.50K | ± 188.13 | ops/s |
| openMetricsWriteToNull | 27.35K | ± 250.02 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 582.75K | ± 2.91K | ops/s |
| prometheusWriteToByteArray | 575.07K | ± 2.09K | ops/s |
| openMetricsWriteToNull | 545.52K | ± 2.18K | ops/s |
| openMetricsWriteToByteArray | 531.39K | ± 12.40K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43253.117   ± 1255.087  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12213.330     ± 48.703  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14127.739    ± 323.052  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      14753.895   ± 3740.770  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48708.144    ± 942.867  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59122.515    ± 778.547  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51495.452    ± 420.312  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6001.966    ± 207.438  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6075.968    ± 124.734  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5912.434     ± 21.669  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        845.138     ± 77.044  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        678.075     ± 10.032  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7020.140    ± 578.260  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14052.944     ± 44.653  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5819.395     ± 12.661  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3003.260    ± 276.961  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.358    ± 134.362  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27347.645    ± 250.021  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27503.838    ± 188.127  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     531391.052  ± 12396.398  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     545522.965   ± 2184.783  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     575074.581   ± 2090.220  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     582746.339   ± 2906.644  ops/s
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
