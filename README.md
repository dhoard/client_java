# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-25T07:13:29Z
- **Commit:** [`9672749`](https://github.com/dhoard/client_java/commit/9672749085f9029ccb7328b3e88e8e78fa29e402)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.22K | ± 1.51K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.80K | ± 615.12 | ops/s | 1.1x slower |
| prometheusAdd | 51.49K | ± 242.88 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.48K | ± 906.10 | ops/s | 1.3x slower |
| simpleclientInc | 6.58K | ± 9.42 | ops/s | 9.9x slower |
| simpleclientAdd | 6.44K | ± 35.79 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.39K | ± 29.64 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.37K | ± 259.45 | ops/s | 19x slower |
| openTelemetryAdd | 3.25K | ± 383.61 | ops/s | 20x slower |
| openTelemetryInc | 3.22K | ± 349.82 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.93K | ± 1.10K | ops/s | **fastest** |
| simpleclient | 4.43K | ± 44.99 | ops/s | 1.3x slower |
| prometheusNative | 2.81K | ± 331.13 | ops/s | 2.1x slower |
| openTelemetryClassic | 733.02 | ± 33.98 | ops/s | 8.1x slower |
| openTelemetryExponential | 629.53 | ± 62.30 | ops/s | 9.4x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.34K | ± 508.50 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.18K | ± 540.08 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 513.69K | ± 6.36K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.20K | ± 4.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 489.09K | ± 3.45K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 486.51K | ± 4.95K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48475.060    ± 906.097  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3254.000    ± 383.608  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3216.308    ± 349.819  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3371.249    ± 259.452  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51493.270    ± 242.880  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65221.909   ± 1510.667  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56799.201    ± 615.122  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6443.247     ± 35.791  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6581.938      ± 9.422  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6386.925     ± 29.641  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        733.017     ± 33.976  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        629.526     ± 62.299  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5929.592   ± 1098.809  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2805.531    ± 331.127  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4430.550     ± 44.994  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23184.810    ± 540.077  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24338.730    ± 508.495  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     486514.846   ± 4948.328  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489090.260   ± 3445.236  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506200.745   ± 4477.623  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     513688.685   ± 6355.578  ops/s
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
