# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-09T07:10:50Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.65K | ± 579.21 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.86K | ± 386.51 | ops/s | 1.2x slower |
| prometheusAdd | 50.58K | ± 398.11 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.17K | ± 1.58K | ops/s | 1.4x slower |
| simpleclientInc | 6.51K | ± 98.27 | ops/s | 10x slower |
| simpleclientAdd | 6.44K | ± 36.49 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.33K | ± 30.29 | ops/s | 11x slower |
| openTelemetryAdd | 3.46K | ± 277.98 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.43K | ± 294.04 | ops/s | 19x slower |
| openTelemetryInc | 3.25K | ± 220.26 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.76K | ± 1.37K | ops/s | **fastest** |
| simpleclient | 4.33K | ± 123.57 | ops/s | 1.3x slower |
| prometheusNative | 2.82K | ± 280.34 | ops/s | 2.0x slower |
| openTelemetryClassic | 769.63 | ± 16.41 | ops/s | 7.5x slower |
| openTelemetryExponential | 641.09 | ± 76.80 | ops/s | 9.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.72K | ± 1.24K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.59K | ± 390.38 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.02K | ± 8.67K | ops/s | **fastest** |
| prometheusWriteToByteArray | 483.74K | ± 3.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 470.46K | ± 3.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 460.93K | ± 2.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49173.958   ± 1576.407  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3457.093    ± 277.977  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3247.589    ± 220.257  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3431.201    ± 294.038  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50579.968    ± 398.111  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66651.568    ± 579.212  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56862.993    ± 386.508  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6441.527     ± 36.494  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6512.980     ± 98.271  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6332.185     ± 30.294  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        769.628     ± 16.413  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        641.085     ± 76.798  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5760.138   ± 1365.004  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2821.799    ± 280.337  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4332.992    ± 123.569  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23593.810    ± 390.382  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23720.421   ± 1241.853  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     460925.054   ± 2528.324  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     470460.876   ± 3100.777  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     483738.522   ± 3919.548  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484021.062   ± 8670.904  ops/s
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
