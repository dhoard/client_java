# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-27T07:24:43Z
- **Commit:** [`d8be554`](https://github.com/dhoard/client_java/commit/d8be5546f2f9ae0ee6f8907cabb7df7d6e85bc95)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.48K | ± 2.00K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.46K | ± 956.85 | ops/s | 1.2x slower |
| prometheusAdd | 48.59K | ± 987.32 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.65K | ± 621.95 | ops/s | 1.3x slower |
| simpleclientInc | 6.14K | ± 47.97 | ops/s | 9.7x slower |
| simpleclientAdd | 6.13K | ± 41.19 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.91K | ± 21.84 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.82K | ± 945.15 | ops/s | 12x slower |
| openTelemetryAdd | 3.99K | ± 921.62 | ops/s | 15x slower |
| openTelemetryInc | 3.90K | ± 331.34 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.67K | ± 1.39K | ops/s | **fastest** |
| simpleclient | 4.19K | ± 37.20 | ops/s | 1.8x slower |
| prometheusNative | 2.97K | ± 243.75 | ops/s | 2.6x slower |
| openTelemetryClassic | 700.52 | ± 15.73 | ops/s | 11x slower |
| openTelemetryExponential | 569.01 | ± 15.07 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.51K | ± 116.92 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.36K | ± 179.12 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 559.28K | ± 4.20K | ops/s | **fastest** |
| prometheusWriteToByteArray | 555.41K | ± 2.75K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 529.29K | ± 3.44K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 509.87K | ± 9.22K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44646.374    ± 621.949  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3990.098    ± 921.620  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3901.783    ± 331.344  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4821.767    ± 945.153  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48588.709    ± 987.319  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59483.975   ± 1995.093  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51463.319    ± 956.851  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6125.379     ± 41.190  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6136.268     ± 47.968  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5909.027     ± 21.836  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        700.524     ± 15.732  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        569.012     ± 15.072  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7670.859   ± 1387.369  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2972.654    ± 243.748  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4193.872     ± 37.201  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27357.546    ± 179.116  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27507.066    ± 116.921  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509865.049   ± 9215.917  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     529293.368   ± 3440.004  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     555410.261   ± 2749.379  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     559283.731   ± 4198.401  ops/s
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
