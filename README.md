# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-26T07:16:55Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.56K | ± 1.04K | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.40K | ± 2.72K | ops/s | 1.2x slower |
| prometheusAdd | 51.27K | ± 332.07 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.93K | ± 591.98 | ops/s | 1.3x slower |
| simpleclientInc | 6.64K | ± 61.61 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.38K | ± 33.05 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 255.65 | ops/s | 10x slower |
| openTelemetryAdd | 3.22K | ± 150.21 | ops/s | 20x slower |
| openTelemetryInc | 3.15K | ± 265.86 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.04K | ± 137.10 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.48K | ± 554.47 | ops/s | **fastest** |
| simpleclient | 4.37K | ± 20.14 | ops/s | 1.3x slower |
| prometheusNative | 2.63K | ± 107.85 | ops/s | 2.1x slower |
| openTelemetryClassic | 745.18 | ± 19.87 | ops/s | 7.4x slower |
| openTelemetryExponential | 637.82 | ± 82.04 | ops/s | 8.6x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 23.94K | ± 986.09 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.52K | ± 601.29 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 517.02K | ± 3.51K | ops/s | **fastest** |
| prometheusWriteToByteArray | 512.79K | ± 7.07K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 491.98K | ± 5.39K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 488.35K | ± 2.97K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49934.302    ± 591.979  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3222.952    ± 150.215  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3151.045    ± 265.864  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3035.397    ± 137.095  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51274.879    ± 332.067  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65559.852   ± 1037.345  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54399.991   ± 2722.703  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6292.696    ± 255.652  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6635.472     ± 61.609  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6384.009     ± 33.054  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        745.176     ± 19.870  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        637.823     ± 82.043  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5478.061    ± 554.474  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2626.858    ± 107.849  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4370.886     ± 20.138  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23520.829    ± 601.294  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23940.449    ± 986.093  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488349.706   ± 2967.800  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     491975.194   ± 5387.005  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     512794.516   ± 7072.211  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     517017.497   ± 3510.516  ops/s
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
