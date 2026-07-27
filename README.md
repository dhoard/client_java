# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-27T07:02:08Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusAdd | 36.62K | ± 1.11K | ops/s | **fastest** |
| prometheusInc | 34.04K | ± 913.99 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 33.95K | ± 1.01K | ops/s | 1.1x slower |
| prometheusNoLabelsInc | 32.98K | ± 562.48 | ops/s | 1.1x slower |
| simpleclientInc | 8.99K | ± 121.31 | ops/s | 4.1x slower |
| simpleclientNoLabelsInc | 8.78K | ± 217.75 | ops/s | 4.2x slower |
| simpleclientAdd | 8.78K | ± 165.10 | ops/s | 4.2x slower |
| openTelemetryAdd | 2.61K | ± 573.12 | ops/s | 14x slower |
| openTelemetryIncNoLabels | 2.17K | ± 271.41 | ops/s | 17x slower |
| openTelemetryInc | 2.06K | ± 107.22 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 8.40K | ± 272.94 | ops/s | **fastest** |
| simpleclient | 5.68K | ± 152.72 | ops/s | 1.5x slower |
| prometheusClassicSingleThread | 4.02K | ± 82.66 | ops/s | 2.1x slower |
| prometheusClassic | 2.89K | ± 464.21 | ops/s | 2.9x slower |
| prometheusNative | 2.44K | ± 299.51 | ops/s | 3.4x slower |
| openTelemetryClassic | 502.80 | ± 58.45 | ops/s | 17x slower |
| openTelemetryExponential | 368.27 | ± 19.15 | ops/s | 23x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.43K | ± 583.85 | ops/s | **fastest** |
| prometheusWriteToNull | 23.31K | ± 1.05K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 352.58K | ± 4.89K | ops/s | **fastest** |
| prometheusWriteToByteArray | 336.97K | ± 9.51K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 315.47K | ± 9.30K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 315.35K | ± 3.23K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      33952.696   ± 1014.778  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2607.680    ± 573.123  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2064.705    ± 107.225  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2170.567    ± 271.408  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36621.011   ± 1111.015  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      34038.484    ± 913.993  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      32979.464    ± 562.477  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8775.703    ± 165.095  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       8990.068    ± 121.313  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8778.794    ± 217.751  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        502.797     ± 58.453  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        368.269     ± 19.146  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2894.150    ± 464.207  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       8396.031    ± 272.940  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4018.511     ± 82.661  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2440.085    ± 299.506  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5676.134    ± 152.718  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23429.359    ± 583.845  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23308.724   ± 1048.403  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     315345.639   ± 3231.933  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     315473.041   ± 9299.521  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     336970.442   ± 9508.917  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     352577.325   ± 4888.930  ops/s
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
