# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-20T06:43:58Z
- **Commit:** [`8d91443`](https://github.com/dhoard/client_java/commit/8d91443665952d8a2585a9e2f220a5811ef2a051)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 60.81K | ± 648.27 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.24K | ± 444.26 | ops/s | 1.2x slower |
| prometheusAdd | 48.17K | ± 283.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.31K | ± 1.94K | ops/s | 1.4x slower |
| simpleclientInc | 6.13K | ± 59.41 | ops/s | 9.9x slower |
| simpleclientAdd | 5.93K | ± 313.00 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 5.90K | ± 28.62 | ops/s | 10x slower |
| openTelemetryInc | 4.41K | ± 1.33K | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.61K | ± 193.89 | ops/s | 17x slower |
| openTelemetryAdd | 3.34K | ± 114.21 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassic | 7.17K | ± 2.01K | ops/s | **fastest** |
| simpleclient | 4.52K | ± 37.53 | ops/s | 1.6x slower |
| prometheusNative | 3.00K | ± 254.10 | ops/s | 2.4x slower |
| openTelemetryClassic | 688.95 | ± 21.38 | ops/s | 10x slower |
| openTelemetryExponential | 528.59 | ± 12.72 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.22K | ± 440.26 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.21K | ± 196.38 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 569.01K | ± 14.98K | ops/s | **fastest** |
| prometheusWriteToByteArray | 566.80K | ± 5.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 543.27K | ± 2.60K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 535.51K | ± 5.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43305.249   ± 1937.233  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3339.731    ± 114.206  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4413.865   ± 1331.941  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3607.538    ± 193.885  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48174.749    ± 283.141  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60808.116    ± 648.269  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52237.139    ± 444.261  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5930.123    ± 312.996  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6132.597     ± 59.408  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5904.236     ± 28.618  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        688.951     ± 21.385  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        528.590     ± 12.723  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7165.725   ± 2005.050  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2998.006    ± 254.105  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4515.995     ± 37.528  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27213.389    ± 196.384  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27221.030    ± 440.262  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     535514.297   ± 5701.171  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     543268.477   ± 2601.532  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     566796.853   ± 5658.134  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     569007.418  ± 14982.420  ops/s
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
