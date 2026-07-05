# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-05T07:10:16Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.03K | ± 323.05 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.68K | ± 372.13 | ops/s | 1.2x slower |
| prometheusAdd | 51.28K | ± 201.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.09K | ± 1.29K | ops/s | 1.4x slower |
| simpleclientInc | 6.56K | ± 40.48 | ops/s | 10x slower |
| simpleclientAdd | 6.33K | ± 195.24 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 26.86 | ops/s | 10x slower |
| openTelemetryInc | 3.15K | ± 313.15 | ops/s | 21x slower |
| openTelemetryIncNoLabels | 3.08K | ± 272.74 | ops/s | 21x slower |
| openTelemetryAdd | 3.01K | ± 193.76 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.02K | ± 2.67K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 22.62 | ops/s | 1.4x slower |
| prometheusNative | 3.03K | ± 235.22 | ops/s | 2.0x slower |
| openTelemetryClassic | 726.94 | ± 7.70 | ops/s | 8.3x slower |
| openTelemetryExponential | 686.76 | ± 106.25 | ops/s | 8.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.71K | ± 344.70 | ops/s | **fastest** |
| prometheusWriteToNull | 23.47K | ± 1.33K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 476.00K | ± 7.07K | ops/s | **fastest** |
| prometheusWriteToNull | 471.75K | ± 5.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 460.99K | ± 6.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 458.23K | ± 6.77K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47090.628   ± 1294.567  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3009.534    ± 193.755  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3150.204    ± 313.152  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3079.626    ± 272.738  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51276.809    ± 201.097  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66031.201    ± 323.053  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56675.409    ± 372.127  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6330.981    ± 195.242  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6560.421     ± 40.475  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6309.629     ± 26.857  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        726.943      ± 7.695  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        686.761    ± 106.248  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6022.405   ± 2674.496  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3027.904    ± 235.221  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4377.751     ± 22.624  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23710.035    ± 344.696  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23469.091   ± 1333.461  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458229.868   ± 6767.468  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460989.036   ± 6890.481  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     475999.520   ± 7065.710  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     471749.791   ± 5742.609  ops/s
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
