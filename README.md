# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-02T05:33:38Z
- **Commit:** [`6beb7fd`](https://github.com/dhoard/client_java/commit/6beb7fd3f26fb1629aae21d9d85d975f63d1a6b8)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1008-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.40K | ± 799.00 | ops/s | **fastest** |
| prometheusNoLabelsInc | 53.66K | ± 4.36K | ops/s | 1.2x slower |
| prometheusAdd | 51.04K | ± 568.83 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.91K | ± 1.06K | ops/s | 1.3x slower |
| simpleclientInc | 6.70K | ± 10.79 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.54K | ± 155.14 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 166.47 | ops/s | 10x slower |
| openTelemetryAdd | 1.42K | ± 262.12 | ops/s | 46x slower |
| openTelemetryInc | 1.36K | ± 184.69 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.23K | ± 49.54 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 346.21 | ops/s | **fastest** |
| simpleclient | 4.42K | ± 84.49 | ops/s | 1.2x slower |
| prometheusNative | 2.96K | ± 335.53 | ops/s | 1.9x slower |
| openTelemetryClassic | 669.03 | ± 18.95 | ops/s | 8.2x slower |
| openTelemetryExponential | 554.28 | ± 32.72 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.70K | ± 2.29K | ops/s | **fastest** |
| openMetricsWriteToNull | 490.26K | ± 1.24K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 487.13K | ± 4.59K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.47K | ± 5.97K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48909.723   ± 1062.100  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1422.203    ± 262.120  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1358.770    ± 184.690  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1227.593     ± 49.539  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51044.192    ± 568.831  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65398.432    ± 798.997  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      53659.420   ± 4355.347  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6321.511    ± 166.466  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6698.312     ± 10.788  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6538.740    ± 155.145  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        669.034     ± 18.948  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.284     ± 32.718  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5494.919    ± 346.211  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2956.897    ± 335.531  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4420.000     ± 84.485  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477471.934   ± 5967.432  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490255.837   ± 1236.213  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487126.593   ± 4591.512  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492696.714   ± 2294.163  ops/s
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
