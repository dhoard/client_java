# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-29T06:22:05Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.69K | ± 1.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.52K | ± 121.02 | ops/s | 1.1x slower |
| prometheusAdd | 51.54K | ± 275.64 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.01K | ± 7.33K | ops/s | 1.5x slower |
| simpleclientInc | 6.51K | ± 62.70 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.35K | ± 11.30 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 219.68 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.24K | ± 198.24 | ops/s | 20x slower |
| openTelemetryInc | 3.13K | ± 118.17 | ops/s | 21x slower |
| openTelemetryAdd | 2.98K | ± 120.10 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.57K | ± 19.35 | ops/s | **fastest** |
| prometheusClassic | 5.47K | ± 1.61K | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 4.60K | ± 20.98 | ops/s | 2.7x slower |
| simpleclient | 4.41K | ± 53.37 | ops/s | 2.9x slower |
| prometheusNative | 2.79K | ± 373.26 | ops/s | 4.5x slower |
| openTelemetryClassic | 790.92 | ± 12.43 | ops/s | 16x slower |
| openTelemetryExponential | 617.16 | ± 83.32 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.37K | ± 547.31 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.28K | ± 925.47 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 501.84K | ± 2.30K | ops/s | **fastest** |
| prometheusWriteToByteArray | 495.88K | ± 5.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 481.67K | ± 1.97K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.20K | ± 4.21K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43007.235   ± 7333.005  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2982.267    ± 120.097  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3125.139    ± 118.170  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3237.249    ± 198.243  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51535.150    ± 275.636  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64687.444   ± 1103.648  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56518.820    ± 121.024  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6318.498    ± 219.682  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6510.970     ± 62.701  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.022     ± 11.298  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        790.924     ± 12.433  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        617.161     ± 83.324  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5465.131   ± 1608.228  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12572.654     ± 19.355  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4595.886     ± 20.975  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2794.731    ± 373.256  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4410.817     ± 53.367  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23283.669    ± 925.467  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23366.745    ± 547.311  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472200.134   ± 4206.274  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     481673.153   ± 1969.480  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     495877.917   ± 5145.333  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     501844.460   ± 2299.174  ops/s
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
