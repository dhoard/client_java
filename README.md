# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-28T14:53:24Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.28K | ± 447.58 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.49K | ± 1.24K | ops/s | 1.2x slower |
| prometheusAdd | 48.47K | ± 536.52 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.54K | ± 564.98 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 17.02K | ± 200.11 | ops/s | 3.5x slower |
| openTelemetryInc | 13.89K | ± 92.81 | ops/s | 4.3x slower |
| openTelemetryAdd | 12.21K | ± 41.79 | ops/s | 4.9x slower |
| simpleclientAdd | 6.14K | ± 32.07 | ops/s | 9.7x slower |
| simpleclientInc | 6.11K | ± 55.97 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.98K | ± 235.49 | ops/s | 9.9x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 13.82K | ± 84.93 | ops/s | **fastest** |
| prometheusClassicSingleThread | 5.85K | ± 105.42 | ops/s | 2.4x slower |
| prometheusClassic | 5.09K | ± 970.41 | ops/s | 2.7x slower |
| simpleclient | 4.54K | ± 27.20 | ops/s | 3.0x slower |
| prometheusNative | 2.78K | ± 173.20 | ops/s | 5.0x slower |
| openTelemetryClassic | 794.98 | ± 78.48 | ops/s | 17x slower |
| openTelemetryExponential | 652.38 | ± 36.93 | ops/s | 21x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.60K | ± 216.85 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.41K | ± 126.80 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 579.32K | ± 3.32K | ops/s | **fastest** |
| prometheusWriteToByteArray | 568.66K | ± 3.31K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 542.71K | ± 9.01K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 530.78K | ± 3.90K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44535.615    ± 564.978  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12206.373     ± 41.793  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13887.661     ± 92.810  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      17020.420    ± 200.115  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48474.608    ± 536.523  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59275.271    ± 447.580  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50485.133   ± 1241.439  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6137.437     ± 32.075  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6114.880     ± 55.969  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5981.928    ± 235.490  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        794.977     ± 78.475  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        652.384     ± 36.929  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5086.578    ± 970.411  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      13815.860     ± 84.930  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5846.355    ± 105.419  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2781.621    ± 173.203  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4537.572     ± 27.195  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27406.139    ± 126.801  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27598.991    ± 216.851  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     530776.261   ± 3902.519  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     542706.784   ± 9010.487  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     568657.358   ± 3309.115  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579323.006   ± 3315.877  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
