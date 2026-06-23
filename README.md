# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-23T07:15:04Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 57.95K | ± 4.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 950.40 | ops/s | 1.1x slower |
| prometheusAdd | 48.67K | ± 1.00K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.45K | ± 395.30 | ops/s | 1.3x slower |
| simpleclientAdd | 6.18K | ± 21.08 | ops/s | 9.4x slower |
| simpleclientInc | 6.08K | ± 5.95 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.88K | ± 11.53 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 4.58K | ± 541.97 | ops/s | 13x slower |
| openTelemetryInc | 4.27K | ± 266.80 | ops/s | 14x slower |
| openTelemetryAdd | 3.59K | ± 135.71 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.73K | ± 832.89 | ops/s | **fastest** |
| simpleclient | 4.53K | ± 39.82 | ops/s | 1.0x slower |
| prometheusNative | 3.18K | ± 79.96 | ops/s | 1.5x slower |
| openTelemetryClassic | 750.34 | ± 34.04 | ops/s | 6.3x slower |
| openTelemetryExponential | 544.24 | ± 11.20 | ops/s | 8.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.52K | ± 194.78 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.99K | ± 334.32 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.55K | ± 4.79K | ops/s | **fastest** |
| prometheusWriteToByteArray | 545.86K | ± 3.43K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 528.61K | ± 3.76K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 516.69K | ± 3.89K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44452.185    ± 395.300  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3592.860    ± 135.708  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4267.648    ± 266.799  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4578.818    ± 541.970  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48667.038   ± 1002.177  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      57952.904   ± 4095.676  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51559.811    ± 950.396  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6183.608     ± 21.083  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6082.002      ± 5.955  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5883.263     ± 11.530  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        750.340     ± 34.040  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.241     ± 11.198  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4734.087    ± 832.886  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3183.151     ± 79.963  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4534.605     ± 39.820  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26991.153    ± 334.324  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27520.488    ± 194.780  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     516693.982   ± 3891.933  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     528611.943   ± 3755.123  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     545861.214   ± 3432.322  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556550.335   ± 4788.296  ops/s
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
