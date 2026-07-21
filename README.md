# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-21T06:21:38Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.18K | ± 1.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.06K | ± 874.58 | ops/s | 1.1x slower |
| prometheusAdd | 51.11K | ± 511.04 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.71K | ± 729.68 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 8.85 | ops/s | 9.8x slower |
| simpleclientAdd | 6.34K | ± 183.75 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.30K | ± 28.23 | ops/s | 10x slower |
| openTelemetryAdd | 3.31K | ± 156.77 | ops/s | 19x slower |
| openTelemetryIncNoLabels | 2.99K | ± 192.34 | ops/s | 21x slower |
| openTelemetryInc | 2.82K | ± 79.60 | ops/s | 23x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.57K | ± 123.13 | ops/s | **fastest** |
| prometheusClassic | 6.12K | ± 1.69K | ops/s | 2.1x slower |
| simpleclient | 4.42K | ± 15.36 | ops/s | 2.8x slower |
| prometheusClassicSingleThread | 4.39K | ± 390.16 | ops/s | 2.9x slower |
| prometheusNative | 2.88K | ± 238.77 | ops/s | 4.4x slower |
| openTelemetryClassic | 745.19 | ± 36.96 | ops/s | 17x slower |
| openTelemetryExponential | 641.01 | ± 56.09 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.46K | ± 448.41 | ops/s | **fastest** |
| prometheusWriteToNull | 24.27K | ± 283.48 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 498.43K | ± 6.94K | ops/s | **fastest** |
| prometheusWriteToByteArray | 488.46K | ± 6.77K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 475.33K | ± 4.21K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 464.88K | ± 3.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49711.145    ± 729.678  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3310.097    ± 156.769  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2823.012     ± 79.597  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2989.220    ± 192.341  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51110.980    ± 511.037  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64180.612   ± 1061.597  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56058.298    ± 874.577  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6337.088    ± 183.754  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6578.796      ± 8.853  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6303.457     ± 28.231  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        745.192     ± 36.958  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        641.007     ± 56.094  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6120.580   ± 1691.229  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12571.727    ± 123.125  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4392.442    ± 390.160  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2875.333    ± 238.772  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4422.093     ± 15.357  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24460.127    ± 448.406  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24272.865    ± 283.478  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     464877.716   ± 3497.364  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     475326.227   ± 4206.914  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488456.092   ± 6771.850  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498434.634   ± 6943.269  ops/s
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
