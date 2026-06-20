# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-20T07:25:59Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.99K | ± 54.02 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.73K | ± 26.79 | ops/s | 1.2x slower |
| prometheusAdd | 48.73K | ± 751.70 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.15K | ± 212.88 | ops/s | 1.4x slower |
| simpleclientInc | 6.15K | ± 96.20 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.91K | ± 24.47 | ops/s | 10x slower |
| simpleclientAdd | 5.89K | ± 194.89 | ops/s | 10x slower |
| openTelemetryAdd | 4.54K | ± 754.90 | ops/s | 13x slower |
| openTelemetryInc | 4.35K | ± 413.61 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 4.33K | ± 536.75 | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.51K | ± 134.18 | ops/s | **fastest** |
| prometheusClassic | 4.46K | ± 554.78 | ops/s | 1.0x slower |
| prometheusNative | 2.93K | ± 213.30 | ops/s | 1.5x slower |
| openTelemetryClassic | 731.26 | ± 14.84 | ops/s | 6.2x slower |
| openTelemetryExponential | 558.66 | ± 6.66 | ops/s | 8.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.34K | ± 346.25 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.26K | ± 320.25 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 586.59K | ± 6.56K | ops/s | **fastest** |
| prometheusWriteToByteArray | 567.88K | ± 4.98K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.36K | ± 3.25K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 536.49K | ± 5.17K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44153.308    ± 212.884  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4542.325    ± 754.896  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4354.985    ± 413.606  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4325.420    ± 536.746  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48731.490    ± 751.698  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59994.727     ± 54.025  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51727.185     ± 26.792  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5888.013    ± 194.887  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6147.397     ± 96.200  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5913.044     ± 24.473  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        731.260     ± 14.837  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.658      ± 6.661  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4461.421    ± 554.776  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2927.058    ± 213.299  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4508.360    ± 134.184  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27259.775    ± 320.248  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27337.242    ± 346.255  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     536489.963   ± 5172.499  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546360.448   ± 3246.621  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     567881.781   ± 4975.643  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     586586.497   ± 6564.250  ops/s
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
