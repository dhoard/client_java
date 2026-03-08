# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-08T05:16:41Z
- **Commit:** [`fc21983`](https://github.com/dhoard/client_java/commit/fc219837f90c194962b33dadab179f19738d75b3)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.23K | ± 1.23K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 124.33 | ops/s | 1.1x slower |
| prometheusAdd | 51.34K | ± 289.71 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.67K | ± 2.09K | ops/s | 1.3x slower |
| simpleclientNoLabelsInc | 6.73K | ± 37.36 | ops/s | 9.7x slower |
| simpleclientInc | 6.64K | ± 112.92 | ops/s | 9.8x slower |
| simpleclientAdd | 6.20K | ± 328.22 | ops/s | 11x slower |
| openTelemetryAdd | 1.58K | ± 190.79 | ops/s | 41x slower |
| openTelemetryInc | 1.29K | ± 84.03 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.20K | ± 35.36 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.08K | ± 1.19K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 42.55 | ops/s | 1.3x slower |
| prometheusNative | 3.01K | ± 350.42 | ops/s | 2.0x slower |
| openTelemetryClassic | 692.12 | ± 43.03 | ops/s | 8.8x slower |
| openTelemetryExponential | 556.95 | ± 29.13 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.36K | ± 2.27K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.04K | ± 4.21K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 463.11K | ± 15.62K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 458.02K | ± 10.06K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49673.725   ± 2091.076  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1582.345    ± 190.788  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1287.017     ± 84.034  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1198.278     ± 35.356  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51336.260    ± 289.711  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65228.685   ± 1233.113  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57239.186    ± 124.327  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6196.564    ± 328.223  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6641.016    ± 112.917  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6728.523     ± 37.360  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        692.123     ± 43.033  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        556.948     ± 29.134  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6077.196   ± 1193.399  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3010.654    ± 350.420  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4539.118     ± 42.550  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     458024.010  ± 10055.415  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     463108.039  ± 15623.580  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485043.990   ± 4205.820  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488363.180   ± 2273.091  ops/s
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
