# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-16T06:35:04Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.59K | ± 688.83 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.84K | ± 960.63 | ops/s | 1.2x slower |
| prometheusAdd | 51.29K | ± 436.67 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.37K | ± 1.48K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 13.49 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.36K | ± 38.12 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 195.37 | ops/s | 11x slower |
| openTelemetryAdd | 3.35K | ± 368.81 | ops/s | 20x slower |
| openTelemetryInc | 3.20K | ± 517.98 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.11K | ± 213.83 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.61K | ± 934.06 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 35.55 | ops/s | 1.5x slower |
| prometheusNative | 2.99K | ± 350.03 | ops/s | 2.2x slower |
| openTelemetryClassic | 788.66 | ± 48.57 | ops/s | 8.4x slower |
| openTelemetryExponential | 604.78 | ± 48.85 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.49K | ± 471.35 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.24K | ± 201.85 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 504.77K | ± 10.91K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.49K | ± 5.12K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 473.10K | ± 5.58K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 465.75K | ± 6.40K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48366.775   ± 1481.864  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3353.677    ± 368.813  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3203.156    ± 517.983  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3111.204    ± 213.829  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51285.883    ± 436.670  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65591.107    ± 688.834  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55836.417    ± 960.634  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6206.822    ± 195.369  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6580.245     ± 13.487  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6363.786     ± 38.120  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        788.661     ± 48.568  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        604.782     ± 48.845  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6613.580    ± 934.057  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2993.304    ± 350.031  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4444.273     ± 35.547  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23241.145    ± 201.847  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23490.062    ± 471.353  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     465752.331   ± 6403.241  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     473095.097   ± 5577.859  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492490.935   ± 5117.394  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504773.180  ± 10913.009  ops/s
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
