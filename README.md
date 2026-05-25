# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-25T07:33:02Z
- **Commit:** [`5ee188f`](https://github.com/dhoard/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.19K | ± 1.62K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.94K | ± 810.90 | ops/s | 1.2x slower |
| prometheusAdd | 51.42K | ± 202.89 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.02K | ± 1.29K | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 33.62 | ops/s | 10.0x slower |
| simpleclientAdd | 6.49K | ± 47.85 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.32K | ± 88.91 | ops/s | 10x slower |
| openTelemetryAdd | 3.32K | ± 574.96 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 2.95K | ± 102.41 | ops/s | 22x slower |
| openTelemetryInc | 2.89K | ± 400.94 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.23K | ± 1.29K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 29.20 | ops/s | 1.2x slower |
| prometheusNative | 2.79K | ± 318.86 | ops/s | 1.9x slower |
| openTelemetryClassic | 744.81 | ± 36.94 | ops/s | 7.0x slower |
| openTelemetryExponential | 573.54 | ± 54.43 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.00K | ± 361.85 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.28K | ± 1.07K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 519.44K | ± 1.80K | ops/s | **fastest** |
| prometheusWriteToByteArray | 508.23K | ± 3.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.96K | ± 4.55K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 486.28K | ± 6.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50021.868   ± 1285.409  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3322.116    ± 574.957  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2894.090    ± 400.943  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2951.403    ± 102.415  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51422.082    ± 202.890  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65194.149   ± 1615.512  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55944.297    ± 810.901  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6486.731     ± 47.854  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6538.988     ± 33.622  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6317.864     ± 88.907  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        744.805     ± 36.939  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        573.543     ± 54.430  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5226.791   ± 1288.749  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2789.129    ± 318.861  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4383.082     ± 29.204  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23281.615   ± 1073.859  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24003.350    ± 361.852  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486278.633   ± 6061.831  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491959.929   ± 4545.631  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     508225.595   ± 3071.830  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     519439.090   ± 1798.317  ops/s
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
