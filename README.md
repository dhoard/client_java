# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-18T05:53:37Z
- **Commit:** [`8d91443`](https://github.com/dhoard/client_java/commit/8d91443665952d8a2585a9e2f220a5811ef2a051)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 75.54K | ± 2.59K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.49K | ± 641.45 | ops/s | 1.1x slower |
| prometheusAdd | 61.61K | ± 397.21 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 53.01K | ± 6.39K | ops/s | 1.4x slower |
| simpleclientInc | 7.91K | ± 70.11 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 7.78K | ± 170.65 | ops/s | 9.7x slower |
| simpleclientAdd | 7.64K | ± 155.75 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 5.74K | ± 1.45K | ops/s | 13x slower |
| openTelemetryInc | 5.71K | ± 1.44K | ops/s | 13x slower |
| openTelemetryAdd | 5.01K | ± 973.18 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 6.89K | ± 1.91K | ops/s | **fastest** |
| simpleclient | 5.82K | ± 49.39 | ops/s | 1.2x slower |
| prometheusNative | 3.69K | ± 376.15 | ops/s | 1.9x slower |
| openTelemetryClassic | 892.34 | ± 4.33 | ops/s | 7.7x slower |
| openTelemetryExponential | 730.83 | ± 44.04 | ops/s | 9.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.43K | ± 191.67 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.94K | ± 267.64 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 699.21K | ± 5.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 674.23K | ± 3.87K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 655.92K | ± 2.78K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 651.75K | ± 6.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      53005.348   ± 6392.517  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5008.425    ± 973.179  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5711.722   ± 1438.586  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5735.955   ± 1449.021  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61606.067    ± 397.213  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75536.447   ± 2590.217  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66488.807    ± 641.452  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7636.299    ± 155.748  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7905.965     ± 70.114  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7776.795    ± 170.648  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        892.338      ± 4.334  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        730.826     ± 44.041  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6889.781   ± 1912.297  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3685.659    ± 376.153  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5823.707     ± 49.394  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34937.568    ± 267.640  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35434.357    ± 191.668  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     651750.547   ± 6105.077  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     655923.993   ± 2778.086  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     674227.414   ± 3866.158  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     699205.940   ± 5893.610  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
