# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-01T08:01:39Z
- **Commit:** [`f0a3b2e`](https://github.com/dhoard/client_java/commit/f0a3b2e46296428952756c95c9037982e7e9baa7)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1015-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.93K | ± 1.08K | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.92K | ± 99.64 | ops/s | 1.2x slower |
| prometheusAdd | 48.24K | ± 347.73 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.31K | ± 1.26K | ops/s | 1.4x slower |
| simpleclientInc | 6.16K | ± 64.83 | ops/s | 9.7x slower |
| simpleclientAdd | 5.94K | ± 208.03 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.90K | ± 8.65 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.22K | ± 457.63 | ops/s | 14x slower |
| openTelemetryInc | 4.10K | ± 291.26 | ops/s | 15x slower |
| openTelemetryAdd | 3.32K | ± 241.10 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.56K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 31.73 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 160.37 | ops/s | 1.8x slower |
| openTelemetryClassic | 708.91 | ± 17.24 | ops/s | 7.8x slower |
| openTelemetryExponential | 583.62 | ± 28.54 | ops/s | 9.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.60K | ± 167.60 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.06K | ± 346.46 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 581.82K | ± 6.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 566.44K | ± 9.52K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 550.58K | ± 2.22K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 540.58K | ± 2.18K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43306.273   ± 1259.144  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3321.353    ± 241.098  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4099.505    ± 291.258  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4215.369    ± 457.634  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48239.093    ± 347.735  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59933.631   ± 1076.106  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50918.685     ± 99.645  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5941.573    ± 208.032  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6159.249     ± 64.828  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5901.976      ± 8.647  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.914     ± 17.243  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        583.621     ± 28.543  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5559.295   ± 1406.638  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3066.224    ± 160.371  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4187.332     ± 31.729  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27064.309    ± 346.464  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27602.410    ± 167.599  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     540580.571   ± 2175.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     550583.255   ± 2218.580  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     566436.351   ± 9523.918  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     581816.459   ± 6754.009  ops/s
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
