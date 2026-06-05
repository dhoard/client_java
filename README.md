# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-05T07:28:39Z
- **Commit:** [`574fb73`](https://github.com/dhoard/client_java/commit/574fb73e4d7eec6bbfd483378600579b966631a6)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.78K | ± 1.75K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.96K | ± 783.15 | ops/s | 1.1x slower |
| prometheusAdd | 51.47K | ± 171.40 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.99K | ± 2.06K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 63.98 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.35K | ± 14.27 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 343.33 | ops/s | 10x slower |
| openTelemetryInc | 3.23K | ± 528.76 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.14K | ± 83.32 | ops/s | 20x slower |
| openTelemetryAdd | 3.11K | ± 379.11 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.77K | ± 1.30K | ops/s | **fastest** |
| simpleclient | 4.42K | ± 64.64 | ops/s | 1.3x slower |
| prometheusNative | 2.93K | ± 300.78 | ops/s | 2.0x slower |
| openTelemetryClassic | 770.80 | ± 11.03 | ops/s | 7.5x slower |
| openTelemetryExponential | 646.99 | ± 55.08 | ops/s | 8.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.00K | ± 959.91 | ops/s | **fastest** |
| openMetricsWriteToNull | 22.80K | ± 1.11K | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 517.14K | ± 3.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 510.34K | ± 5.83K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 487.85K | ± 4.55K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 487.15K | ± 4.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48994.778   ± 2063.914  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3111.214    ± 379.106  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3229.173    ± 528.756  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3144.088     ± 83.318  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51469.743    ± 171.399  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63777.222   ± 1748.131  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55958.759    ± 783.150  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6206.932    ± 343.325  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6539.930     ± 63.985  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.944     ± 14.270  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        770.804     ± 11.027  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        646.985     ± 55.077  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5769.657   ± 1300.263  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2928.571    ± 300.776  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4421.188     ± 64.637  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22802.495   ± 1105.357  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23999.525    ± 959.909  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     487152.412   ± 4481.256  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     487850.365   ± 4553.479  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     510336.289   ± 5827.934  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     517144.079   ± 3859.298  ops/s
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
