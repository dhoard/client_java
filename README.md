# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-01T06:40:21Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.54K | ± 319.62 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.01K | ± 2.01K | ops/s | 1.2x slower |
| prometheusAdd | 48.31K | ± 162.31 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.92K | ± 4.50K | ops/s | 1.5x slower |
| simpleclientInc | 6.09K | ± 20.18 | ops/s | 9.8x slower |
| simpleclientAdd | 6.04K | ± 207.31 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.91K | ± 30.36 | ops/s | 10x slower |
| openTelemetryInc | 4.26K | ± 1.33K | ops/s | 14x slower |
| openTelemetryAdd | 4.12K | ± 888.11 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 3.62K | ± 287.49 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.50K | ± 70.75 | ops/s | **fastest** |
| prometheusClassic | 6.25K | ± 1.80K | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 6.01K | ± 119.33 | ops/s | 2.4x slower |
| simpleclient | 4.52K | ± 105.59 | ops/s | 3.2x slower |
| prometheusNative | 3.00K | ± 150.51 | ops/s | 4.8x slower |
| openTelemetryClassic | 674.96 | ± 5.19 | ops/s | 21x slower |
| openTelemetryExponential | 530.11 | ± 14.42 | ops/s | 27x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 27.31K | ± 220.98 | ops/s | **fastest** |
| prometheusWriteToNull | 27.12K | ± 799.26 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 549.68K | ± 10.81K | ops/s | **fastest** |
| prometheusWriteToByteArray | 547.68K | ± 6.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 527.12K | ± 3.89K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.12K | ± 2.91K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40917.627   ± 4498.691  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4117.438    ± 888.108  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4259.530   ± 1329.732  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3620.801    ± 287.490  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48307.734    ± 162.310  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59537.606    ± 319.624  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50010.615   ± 2006.507  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6035.214    ± 207.312  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6090.508     ± 20.179  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5911.046     ± 30.358  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.959      ± 5.188  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        530.106     ± 14.423  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6252.674   ± 1799.008  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14501.316     ± 70.751  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       6013.005    ± 119.327  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2997.649    ± 150.507  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4519.683    ± 105.586  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27308.815    ± 220.978  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27121.590    ± 799.264  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519118.377   ± 2914.026  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     527123.858   ± 3892.316  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     547682.910   ± 6127.063  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549683.087  ± 10805.459  ops/s
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
