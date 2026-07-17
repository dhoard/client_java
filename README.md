# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-17T06:08:25Z
- **Commit:** [`be2bc20`](https://github.com/dhoard/client_java/commit/be2bc20fdf941be85a0ad020f5f405af623a7883)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusAdd | 35.69K | ± 714.94 | ops/s | **fastest** |
| prometheusInc | 35.39K | ± 683.45 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 34.74K | ± 802.86 | ops/s | 1.0x slower |
| prometheusNoLabelsInc | 33.92K | ± 524.73 | ops/s | 1.1x slower |
| simpleclientInc | 9.19K | ± 98.82 | ops/s | 3.9x slower |
| simpleclientNoLabelsInc | 9.04K | ± 81.44 | ops/s | 3.9x slower |
| simpleclientAdd | 8.91K | ± 115.53 | ops/s | 4.0x slower |
| openTelemetryIncNoLabels | 2.47K | ± 473.03 | ops/s | 14x slower |
| openTelemetryAdd | 2.29K | ± 599.65 | ops/s | 16x slower |
| openTelemetryInc | 2.11K | ± 234.44 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| simpleclient | 6.07K | ± 68.25 | ops/s | **fastest** |
| prometheusClassic | 3.23K | ± 1.85K | ops/s | 1.9x slower |
| prometheusNative | 2.17K | ± 322.73 | ops/s | 2.8x slower |
| openTelemetryClassic | 503.98 | ± 105.52 | ops/s | 12x slower |
| openTelemetryExponential | 388.22 | ± 40.64 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 24.93K | ± 471.81 | ops/s | **fastest** |
| prometheusWriteToNull | 24.92K | ± 376.24 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToByteArray | 349.80K | ± 3.74K | ops/s | **fastest** |
| prometheusWriteToNull | 345.43K | ± 3.83K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 332.61K | ± 2.33K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 324.45K | ± 5.10K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      34737.389    ± 802.861  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2286.263    ± 599.652  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2106.866    ± 234.437  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       2470.012    ± 473.026  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      35691.750    ± 714.935  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35386.071    ± 683.446  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      33921.821    ± 524.732  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8911.472    ± 115.532  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9194.356     ± 98.816  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       9044.643     ± 81.443  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        503.981    ± 105.522  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        388.216     ± 40.643  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3233.936   ± 1851.661  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2166.307    ± 322.730  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6067.542     ± 68.255  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24930.851    ± 471.814  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24918.117    ± 376.242  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     332606.021   ± 2326.570  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     324453.442   ± 5100.283  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     349797.749   ± 3739.866  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     345427.357   ± 3834.939  ops/s
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
