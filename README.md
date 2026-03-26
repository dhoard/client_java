# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-26T05:38:59Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.07K | ± 1.70K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.90K | ± 288.39 | ops/s | 1.1x slower |
| prometheusAdd | 51.78K | ± 95.70 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.76K | ± 3.38K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 10.08 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.70K | ± 9.54 | ops/s | 9.7x slower |
| simpleclientAdd | 6.40K | ± 238.20 | ops/s | 10x slower |
| openTelemetryInc | 1.36K | ± 227.18 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.35K | ± 156.31 | ops/s | 48x slower |
| openTelemetryAdd | 1.33K | ± 75.78 | ops/s | 49x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.16K | ± 1.41K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 36.37 | ops/s | 1.1x slower |
| prometheusNative | 2.85K | ± 221.23 | ops/s | 1.8x slower |
| openTelemetryClassic | 677.62 | ± 50.42 | ops/s | 7.6x slower |
| openTelemetryExponential | 582.70 | ± 24.32 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 489.57K | ± 2.95K | ops/s | **fastest** |
| prometheusWriteToNull | 487.24K | ± 2.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 472.84K | ± 3.09K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 467.02K | ± 3.29K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46761.451   ± 3378.501  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1325.617     ± 75.782  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1363.958    ± 227.184  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1347.486    ± 156.313  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51783.596     ± 95.705  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65072.410   ± 1698.962  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56903.592    ± 288.386  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6399.162    ± 238.202  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6780.327     ± 10.079  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6696.881      ± 9.537  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        677.619     ± 50.415  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        582.700     ± 24.322  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5160.657   ± 1406.586  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2845.066    ± 221.233  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4549.726     ± 36.368  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     467017.613   ± 3292.508  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     472843.812   ± 3090.279  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     489567.385   ± 2945.206  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487242.636   ± 2717.185  ops/s
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
