# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-19T05:24:38Z
- **Commit:** [`5093750`](https://github.com/dhoard/client_java/commit/50937500b4cfa35825a4441860b256df819c918c)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 31.61K | ± 17.90 | ops/s | **fastest** |
| prometheusNoLabelsInc | 31.12K | ± 30.13 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 28.58K | ± 516.31 | ops/s | 1.1x slower |
| prometheusAdd | 27.47K | ± 1.66K | ops/s | 1.2x slower |
| simpleclientInc | 6.93K | ± 61.54 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.87K | ± 236.43 | ops/s | 4.6x slower |
| simpleclientAdd | 6.55K | ± 240.28 | ops/s | 4.8x slower |
| openTelemetryAdd | 1.42K | ± 89.01 | ops/s | 22x slower |
| openTelemetryIncNoLabels | 1.36K | ± 68.00 | ops/s | 23x slower |
| openTelemetryInc | 1.33K | ± 56.93 | ops/s | 24x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.58K | ± 79.16 | ops/s | **fastest** |
| prometheusClassic | 3.29K | ± 1.80K | ops/s | 1.4x slower |
| prometheusNative | 2.41K | ± 255.77 | ops/s | 1.9x slower |
| openTelemetryClassic | 520.36 | ± 35.23 | ops/s | 8.8x slower |
| openTelemetryExponential | 401.12 | ± 18.23 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 326.67K | ± 2.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 324.00K | ± 1.45K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 307.94K | ± 2.50K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 304.23K | ± 1.53K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      28582.687    ± 516.307  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1416.457     ± 89.009  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1334.463     ± 56.926  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1361.500     ± 67.997  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27470.542   ± 1663.593  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31611.683     ± 17.900  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      31124.633     ± 30.135  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6553.225    ± 240.280  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6929.954     ± 61.538  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6866.059    ± 236.430  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        520.360     ± 35.233  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        401.117     ± 18.233  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3290.521   ± 1797.884  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2410.694    ± 255.771  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4581.424     ± 79.159  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     304229.734   ± 1529.214  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     307937.116   ± 2501.460  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     323995.533   ± 1447.610  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     326672.728   ± 2194.645  ops/s
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
