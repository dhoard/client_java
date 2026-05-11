# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-11T07:05:59Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 31.19K | ± 338.75 | ops/s | **fastest** |
| codahaleIncNoLabels | 31.15K | ± 749.86 | ops/s | 1.0x slower |
| prometheusInc | 30.95K | ± 1.34K | ops/s | 1.0x slower |
| prometheusAdd | 27.72K | ± 1.28K | ops/s | 1.1x slower |
| simpleclientInc | 6.83K | ± 118.02 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.58K | ± 131.14 | ops/s | 4.7x slower |
| simpleclientAdd | 6.51K | ± 196.81 | ops/s | 4.8x slower |
| openTelemetryIncNoLabels | 2.78K | ± 275.82 | ops/s | 11x slower |
| openTelemetryAdd | 2.55K | ± 387.64 | ops/s | 12x slower |
| openTelemetryInc | 2.45K | ± 78.32 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.45K | ± 46.90 | ops/s | **fastest** |
| prometheusClassic | 3.14K | ± 170.76 | ops/s | 1.4x slower |
| prometheusNative | 2.32K | ± 78.97 | ops/s | 1.9x slower |
| openTelemetryClassic | 645.54 | ± 8.61 | ops/s | 6.9x slower |
| openTelemetryExponential | 446.85 | ± 26.97 | ops/s | 9.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 18.31K | ± 70.94 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.29K | ± 123.61 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 318.33K | ± 2.01K | ops/s | **fastest** |
| prometheusWriteToByteArray | 317.58K | ± 1.61K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.35K | ± 2.20K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 294.77K | ± 1.61K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      31149.158    ± 749.861  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2549.442    ± 387.636  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2452.248     ± 78.318  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2782.121    ± 275.824  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27720.793   ± 1279.193  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      30947.376   ± 1335.958  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31187.418    ± 338.754  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6513.196    ± 196.813  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6827.292    ± 118.017  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6580.038    ± 131.144  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        645.537      ± 8.609  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        446.846     ± 26.972  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3142.611    ± 170.762  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2318.562     ± 78.966  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4445.045     ± 46.900  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18289.775    ± 123.608  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18313.676     ± 70.944  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     294768.507   ± 1611.239  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296354.409   ± 2202.624  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     317577.678   ± 1613.171  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318328.376   ± 2013.838  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
