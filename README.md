# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-16T05:58:23Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.98K | ± 1.83K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.40K | ± 1.04K | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 109.10 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.84K | ± 220.80 | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 186.82 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 223.33 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 241.45 | ops/s | 11x slower |
| openTelemetryAdd | 1.51K | ± 215.28 | ops/s | 44x slower |
| openTelemetryInc | 1.39K | ± 155.13 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.20K | ± 100.36 | ops/s | 55x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.04K | ± 687.24 | ops/s | **fastest** |
| simpleclient | 4.44K | ± 64.79 | ops/s | 1.1x slower |
| prometheusNative | 2.78K | ± 281.43 | ops/s | 1.8x slower |
| openTelemetryClassic | 704.30 | ± 9.25 | ops/s | 7.1x slower |
| openTelemetryExponential | 565.84 | ± 12.50 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.66K | ± 3.82K | ops/s | **fastest** |
| openMetricsWriteToNull | 492.65K | ± 799.15 | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 488.34K | ± 2.94K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 477.70K | ± 6.25K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47842.489    ± 220.796  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1505.129    ± 215.280  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1390.202    ± 155.131  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1202.218    ± 100.357  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51583.948    ± 109.097  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65975.162   ± 1830.958  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56398.905   ± 1040.615  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.573    ± 241.451  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6532.314    ± 186.822  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6471.941    ± 223.332  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        704.303      ± 9.250  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        565.844     ± 12.504  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5035.610    ± 687.240  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2780.992    ± 281.428  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4442.104     ± 64.788  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     477696.305   ± 6245.997  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     492650.327    ± 799.151  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     488344.545   ± 2940.493  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497663.370   ± 3823.482  ops/s
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
