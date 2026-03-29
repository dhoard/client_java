# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-29T05:43:27Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.24K | ± 1.38K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.23K | ± 2.60K | ops/s | 1.2x slower |
| prometheusAdd | 51.63K | ± 110.85 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.88K | ± 608.02 | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.46K | ± 204.91 | ops/s | 10x slower |
| simpleclientInc | 6.42K | ± 225.23 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 274.55 | ops/s | 10x slower |
| openTelemetryAdd | 1.41K | ± 260.54 | ops/s | 46x slower |
| openTelemetryInc | 1.39K | ± 158.11 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.24K | ± 20.05 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.30K | ± 2.80K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 30.98 | ops/s | 1.4x slower |
| prometheusNative | 2.94K | ± 343.16 | ops/s | 2.1x slower |
| openTelemetryClassic | 698.09 | ± 7.20 | ops/s | 9.0x slower |
| openTelemetryExponential | 555.84 | ± 23.41 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 484.53K | ± 4.40K | ops/s | **fastest** |
| prometheusWriteToNull | 482.98K | ± 2.02K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 474.22K | ± 6.27K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.82K | ± 3.75K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49877.540    ± 608.020  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1410.996    ± 260.536  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1394.542    ± 158.111  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1241.748     ± 20.048  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51627.059    ± 110.852  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65235.426   ± 1383.473  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55231.415   ± 2603.670  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6315.403    ± 274.554  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6423.868    ± 225.233  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6460.133    ± 204.906  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        698.094      ± 7.200  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        555.844     ± 23.412  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6297.076   ± 2795.087  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2943.378    ± 343.163  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4463.518     ± 30.977  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469818.901   ± 3753.388  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     474221.686   ± 6270.397  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     484530.448   ± 4396.499  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     482977.954   ± 2015.241  ops/s
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
