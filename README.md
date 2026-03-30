# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-30T05:51:21Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.36K | ± 297.24 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.97K | ± 321.50 | ops/s | 1.2x slower |
| prometheusAdd | 51.19K | ± 425.80 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 1.45K | ops/s | 1.4x slower |
| simpleclientInc | 6.69K | ± 34.50 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.53K | ± 142.17 | ops/s | 10x slower |
| simpleclientAdd | 6.21K | ± 208.62 | ops/s | 11x slower |
| openTelemetryIncNoLabels | 1.31K | ± 111.11 | ops/s | 51x slower |
| openTelemetryAdd | 1.25K | ± 55.17 | ops/s | 53x slower |
| openTelemetryInc | 1.22K | ± 45.72 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.84K | ± 592.45 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 41.28 | ops/s | 1.1x slower |
| prometheusNative | 2.77K | ± 300.58 | ops/s | 1.7x slower |
| openTelemetryClassic | 708.83 | ± 28.43 | ops/s | 6.8x slower |
| openTelemetryExponential | 544.96 | ± 38.69 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 481.81K | ± 3.18K | ops/s | **fastest** |
| openMetricsWriteToNull | 478.69K | ± 6.14K | ops/s | 1.0x slower |
| prometheusWriteToNull | 469.70K | ± 19.29K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 469.55K | ± 5.96K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48474.246   ± 1446.567  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.430     ± 55.171  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1218.990     ± 45.723  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1307.110    ± 111.114  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51186.560    ± 425.799  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66357.393    ± 297.236  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56969.841    ± 321.496  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6209.043    ± 208.615  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6687.836     ± 34.499  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6530.529    ± 142.174  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        708.825     ± 28.434  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.962     ± 38.688  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4838.255    ± 592.449  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2769.536    ± 300.584  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4443.988     ± 41.278  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     469551.162   ± 5963.811  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     478686.547   ± 6142.870  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481807.647   ± 3184.046  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     469696.142  ± 19288.874  ops/s
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
