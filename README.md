# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-18T05:28:40Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.17K | ± 1.45K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.95K | ± 436.21 | ops/s | 1.1x slower |
| prometheusAdd | 51.63K | ± 222.43 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.85K | ± 1.21K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 188.86 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 6.44K | ± 200.57 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 185.34 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 1.32K | ± 108.45 | ops/s | 49x slower |
| openTelemetryInc | 1.28K | ± 50.11 | ops/s | 51x slower |
| openTelemetryAdd | 1.22K | ± 31.74 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.59K | ± 1.56K | ops/s | **fastest** |
| simpleclient | 4.47K | ± 101.91 | ops/s | 1.2x slower |
| prometheusNative | 3.21K | ± 82.91 | ops/s | 1.7x slower |
| openTelemetryClassic | 714.59 | ± 35.71 | ops/s | 7.8x slower |
| openTelemetryExponential | 567.57 | ± 37.08 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.87K | ± 1.40K | ops/s | **fastest** |
| openMetricsWriteToNull | 489.88K | ± 3.61K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 487.88K | ± 4.16K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.93K | ± 5.84K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48848.108   ± 1212.868  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1220.883     ± 31.735  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1282.576     ± 50.113  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1318.053    ± 108.447  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51627.477    ± 222.427  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65168.990   ± 1450.976  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56953.721    ± 436.207  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6295.246    ± 185.337  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6548.494    ± 188.857  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6443.564    ± 200.566  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        714.588     ± 35.705  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.568     ± 37.078  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5588.205   ± 1561.926  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3213.112     ± 82.911  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4470.572    ± 101.910  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476929.534   ± 5843.471  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     489878.519   ± 3612.166  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487876.910   ± 4163.375  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492872.881   ± 1397.747  ops/s
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
