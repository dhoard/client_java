# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-22T08:26:32Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.18K | ± 707.31 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.35K | ± 2.46K | ops/s | 1.2x slower |
| prometheusAdd | 51.37K | ± 331.90 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.98K | ± 932.44 | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 34.58 | ops/s | 10x slower |
| simpleclientAdd | 6.34K | ± 243.96 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.30K | ± 44.91 | ops/s | 11x slower |
| openTelemetryAdd | 3.48K | ± 173.89 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 3.47K | ± 415.38 | ops/s | 19x slower |
| openTelemetryInc | 3.34K | ± 556.53 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.96K | ± 2.22K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 34.95 | ops/s | 1.4x slower |
| prometheusNative | 2.78K | ± 272.89 | ops/s | 2.1x slower |
| openTelemetryClassic | 796.17 | ± 14.16 | ops/s | 7.5x slower |
| openTelemetryExponential | 608.84 | ± 71.33 | ops/s | 9.8x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.16K | ± 240.60 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.88K | ± 708.16 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.90K | ± 4.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.43K | ± 6.67K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.03K | ± 4.55K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.33K | ± 5.03K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48981.297    ± 932.439  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3479.349    ± 173.889  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3339.760    ± 556.530  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3465.463    ± 415.379  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51369.340    ± 331.900  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66182.132    ± 707.306  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55352.733   ± 2460.171  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6340.215    ± 243.960  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.297     ± 34.577  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6302.751     ± 44.909  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        796.174     ± 14.157  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        608.843     ± 71.333  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5957.007   ± 2215.904  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2777.044    ± 272.893  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4378.448     ± 34.948  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23877.437    ± 708.159  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24159.928    ± 240.597  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471334.857   ± 5029.543  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477027.025   ± 4548.664  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495434.673   ± 6670.280  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497904.212   ± 4324.208  ops/s
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
