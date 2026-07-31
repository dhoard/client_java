# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-31T06:47:30Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.98K | ± 1.91K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.11K | ± 917.34 | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 485.13 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.24K | ± 1.56K | ops/s | 1.3x slower |
| simpleclientInc | 6.61K | ± 54.38 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.38K | ± 27.85 | ops/s | 10x slower |
| simpleclientAdd | 6.25K | ± 345.85 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.52K | ± 404.41 | ops/s | 18x slower |
| openTelemetryAdd | 3.11K | ± 373.59 | ops/s | 21x slower |
| openTelemetryInc | 2.94K | ± 145.94 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.52K | ± 83.09 | ops/s | **fastest** |
| prometheusClassic | 6.00K | ± 1.36K | ops/s | 2.1x slower |
| prometheusClassicSingleThread | 4.59K | ± 14.22 | ops/s | 2.7x slower |
| simpleclient | 4.40K | ± 36.38 | ops/s | 2.8x slower |
| prometheusNative | 3.05K | ± 264.39 | ops/s | 4.1x slower |
| openTelemetryClassic | 717.14 | ± 48.25 | ops/s | 17x slower |
| openTelemetryExponential | 691.86 | ± 64.65 | ops/s | 18x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.89K | ± 459.61 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.54K | ± 661.35 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 509.16K | ± 6.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 502.76K | ± 3.13K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.57K | ± 2.24K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.80K | ± 4.20K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48235.686   ± 1555.016  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3110.679    ± 373.593  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2937.007    ± 145.940  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3515.081    ± 404.414  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51213.054    ± 485.134  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64976.576   ± 1911.250  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56111.009    ± 917.342  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6247.619    ± 345.847  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6610.798     ± 54.384  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6384.753     ± 27.854  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.138     ± 48.252  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        691.859     ± 64.649  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6002.175   ± 1362.332  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12515.187     ± 83.089  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4593.135     ± 14.222  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3045.534    ± 264.391  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4398.040     ± 36.381  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23544.605    ± 661.349  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23886.626    ± 459.606  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479795.217   ± 4197.546  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488571.704   ± 2235.047  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502764.917   ± 3131.649  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     509164.810   ± 6445.825  ops/s
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
