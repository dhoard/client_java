# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-04T07:44:18Z
- **Commit:** [`574fb73`](https://github.com/dhoard/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.39K | ± 911.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.45K | ± 443.60 | ops/s | 1.1x slower |
| prometheusAdd | 48.45K | ± 166.75 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.96K | ± 192.76 | ops/s | 1.3x slower |
| simpleclientInc | 6.20K | ± 3.20 | ops/s | 9.4x slower |
| simpleclientAdd | 6.13K | ± 57.50 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.92K | ± 23.84 | ops/s | 9.9x slower |
| openTelemetryInc | 4.77K | ± 1.13K | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.05K | ± 554.78 | ops/s | 14x slower |
| openTelemetryAdd | 3.99K | ± 766.34 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.89K | ± 553.47 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 37.55 | ops/s | 1.1x slower |
| prometheusNative | 2.89K | ± 186.53 | ops/s | 1.7x slower |
| openTelemetryClassic | 735.72 | ± 45.06 | ops/s | 6.7x slower |
| openTelemetryExponential | 563.99 | ± 41.95 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.50K | ± 355.23 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.43K | ± 123.58 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.50K | ± 6.06K | ops/s | **fastest** |
| prometheusWriteToByteArray | 558.57K | ± 8.35K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 539.16K | ± 6.60K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 532.63K | ± 4.60K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43955.222    ± 192.762  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3987.163    ± 766.337  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4767.831   ± 1131.339  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4045.388    ± 554.781  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48449.053    ± 166.752  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58387.660    ± 911.682  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51448.800    ± 443.601  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6131.112     ± 57.498  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6203.174      ± 3.202  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5923.238     ± 23.842  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        735.725     ± 45.055  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.992     ± 41.949  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4893.580    ± 553.470  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2888.756    ± 186.525  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4372.604     ± 37.554  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27434.853    ± 123.579  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27502.986    ± 355.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     532626.129   ± 4598.090  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539162.873   ± 6604.631  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     558568.208   ± 8350.889  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581499.356   ± 6057.371  ops/s
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
