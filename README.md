# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-18T05:26:12Z
- **Commit:** [`5093750`](https://github.com/dhoard/client_java/commit/50937500b4cfa35825a4441860b256df819c918c)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.56K | ± 1.52K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.83K | ± 352.18 | ops/s | 1.1x slower |
| prometheusAdd | 51.40K | ± 605.94 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.20K | ± 1.47K | ops/s | 1.3x slower |
| simpleclientInc | 6.65K | ± 173.05 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.57K | ± 214.30 | ops/s | 9.8x slower |
| simpleclientAdd | 5.99K | ± 186.69 | ops/s | 11x slower |
| openTelemetryInc | 1.30K | ± 58.92 | ops/s | 50x slower |
| openTelemetryAdd | 1.29K | ± 74.76 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.24K | ± 19.26 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.36K | ± 1.59K | ops/s | **fastest** |
| simpleclient | 4.56K | ± 26.12 | ops/s | 1.2x slower |
| prometheusNative | 3.07K | ± 206.20 | ops/s | 1.7x slower |
| openTelemetryClassic | 697.74 | ± 36.90 | ops/s | 7.7x slower |
| openTelemetryExponential | 566.97 | ± 17.73 | ops/s | 9.5x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.89K | ± 2.90K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.33K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.63K | ± 4.11K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.08K | ± 4.95K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48204.455   ± 1470.223  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1289.559     ± 74.760  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1297.926     ± 58.919  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1243.173     ± 19.255  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51395.262    ± 605.945  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64560.542   ± 1523.572  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56828.237    ± 352.177  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5988.607    ± 186.694  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6652.439    ± 173.054  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6573.215    ± 214.303  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.744     ± 36.902  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        566.974     ± 17.733  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5360.868   ± 1591.243  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.586    ± 206.204  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4562.268     ± 26.116  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477084.590   ± 4947.853  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479625.855   ± 4113.559  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485327.483   ± 3064.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497893.841   ± 2895.333  ops/s
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
