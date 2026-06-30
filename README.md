# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-30T07:17:33Z
- **Commit:** [`2a2c73d`](https://github.com/dhoard/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 67.10K | ± 1.24K | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.40K | ± 816.94 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 60.15K | ± 827.70 | ops/s | 1.1x slower |
| prometheusAdd | 58.35K | ± 2.12K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 10.36K | ± 307.85 | ops/s | 6.5x slower |
| simpleclientInc | 10.32K | ± 474.14 | ops/s | 6.5x slower |
| simpleclientAdd | 10.24K | ± 245.28 | ops/s | 6.6x slower |
| openTelemetryIncNoLabels | 6.70K | ± 178.57 | ops/s | 10x slower |
| openTelemetryInc | 5.37K | ± 330.65 | ops/s | 12x slower |
| openTelemetryAdd | 4.61K | ± 143.70 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 8.44K | ± 2.28K | ops/s | **fastest** |
| simpleclient | 6.81K | ± 233.41 | ops/s | 1.2x slower |
| prometheusNative | 5.03K | ± 584.32 | ops/s | 1.7x slower |
| openTelemetryClassic | 900.57 | ± 22.91 | ops/s | 9.4x slower |
| openTelemetryExponential | 713.89 | ± 20.73 | ops/s | 12x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 33.12K | ± 603.30 | ops/s | **fastest** |
| openMetricsWriteToNull | 32.87K | ± 603.85 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 718.87K | ± 10.44K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 698.46K | ± 18.44K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 695.60K | ± 24.56K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 644.50K | ± 35.71K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      60150.791    ± 827.698  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4606.057    ± 143.702  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5370.372    ± 330.645  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       6703.836    ± 178.566  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58351.851   ± 2116.751  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      67096.368   ± 1241.922  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66398.150    ± 816.940  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10236.380    ± 245.277  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10317.518    ± 474.144  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10358.313    ± 307.845  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        900.567     ± 22.909  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        713.889     ± 20.729  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8438.661   ± 2275.908  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5033.947    ± 584.323  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6809.401    ± 233.410  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      32871.190    ± 603.847  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33121.495    ± 603.303  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     698459.849  ± 18437.031  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     644497.228  ± 35710.607  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     695597.063  ± 24555.340  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     718871.494  ± 10441.514  ops/s
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
