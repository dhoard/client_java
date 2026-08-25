# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-25T04:14:49Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusNoLabelsInc | 66.44K | ± 534.94 | ops/s | **fastest** |
| prometheusInc | 64.21K | ± 14.84K | ops/s | 1.0x slower |
| prometheusAdd | 62.93K | ± 861.22 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 58.66K | ± 982.27 | ops/s | 1.1x slower |
| openTelemetryIncNoLabels | 21.90K | ± 277.58 | ops/s | 3.0x slower |
| openTelemetryInc | 17.76K | ± 247.66 | ops/s | 3.7x slower |
| openTelemetryAdd | 15.67K | ± 116.91 | ops/s | 4.2x slower |
| simpleclientInc | 7.85K | ± 23.17 | ops/s | 8.5x slower |
| simpleclientAdd | 7.73K | ± 181.27 | ops/s | 8.6x slower |
| simpleclientNoLabelsInc | 7.62K | ± 31.31 | ops/s | 8.7x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 18.14K | ± 36.40 | ops/s | **fastest** |
| prometheusClassic | 11.00K | ± 2.24K | ops/s | 1.6x slower |
| prometheusClassicSingleThread | 7.39K | ± 176.15 | ops/s | 2.5x slower |
| simpleclient | 5.74K | ± 217.59 | ops/s | 3.2x slower |
| prometheusNative | 3.66K | ± 329.04 | ops/s | 5.0x slower |
| openTelemetryClassic | 1.05K | ± 104.49 | ops/s | 17x slower |
| openTelemetryExponential | 890.57 | ± 7.61 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.43K | ± 257.90 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.26K | ± 106.33 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 701.48K | ± 24.49K | ops/s | **fastest** |
| prometheusWriteToByteArray | 687.26K | ± 10.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 654.24K | ± 16.58K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 640.28K | ± 7.58K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      58655.072    ± 982.270  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15673.860    ± 116.907  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17758.411    ± 247.660  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21901.848    ± 277.582  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62929.700    ± 861.224  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64211.504  ± 14841.691  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66442.634    ± 534.937  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7729.324    ± 181.272  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7850.304     ± 23.174  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7618.339     ± 31.307  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1050.934    ± 104.492  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        890.575      ± 7.615  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      11004.908   ± 2243.544  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18136.548     ± 36.398  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7394.728    ± 176.152  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3657.169    ± 329.039  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5741.438    ± 217.594  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35259.869    ± 106.328  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35429.135    ± 257.903  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     640279.906   ± 7582.039  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     654237.081  ± 16580.506  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     687256.194  ± 10444.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     701478.312  ± 24489.264  ops/s
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
