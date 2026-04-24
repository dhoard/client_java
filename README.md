# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-24T06:01:21Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.02K | ± 2.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.10K | ± 432.71 | ops/s | 1.1x slower |
| prometheusAdd | 48.20K | ± 356.49 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.98K | ± 617.02 | ops/s | 1.3x slower |
| simpleclientInc | 6.33K | ± 49.66 | ops/s | 9.2x slower |
| simpleclientNoLabelsInc | 6.28K | ± 37.92 | ops/s | 9.2x slower |
| simpleclientAdd | 5.82K | ± 323.68 | ops/s | 10.0x slower |
| openTelemetryAdd | 1.31K | ± 66.13 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.31K | ± 34.01 | ops/s | 44x slower |
| openTelemetryInc | 1.24K | ± 73.64 | ops/s | 47x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.89K | ± 2.28K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 29.03 | ops/s | 1.3x slower |
| prometheusNative | 2.96K | ± 210.62 | ops/s | 2.0x slower |
| openTelemetryClassic | 603.25 | ± 44.04 | ops/s | 9.8x slower |
| openTelemetryExponential | 521.41 | ± 23.12 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 551.55K | ± 3.75K | ops/s | **fastest** |
| prometheusWriteToByteArray | 542.17K | ± 3.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 531.43K | ± 1.98K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 527.16K | ± 2.35K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43976.951    ± 617.023  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1314.546     ± 66.127  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1235.620     ± 73.642  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1312.003     ± 34.014  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48197.315    ± 356.492  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58018.798   ± 2256.565  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52102.783    ± 432.713  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5822.415    ± 323.680  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6331.439     ± 49.659  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6275.818     ± 37.922  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        603.246     ± 44.039  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        521.414     ± 23.124  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5886.238   ± 2279.532  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.873    ± 210.615  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4543.135     ± 29.025  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     527161.172   ± 2350.961  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     531428.646   ± 1980.150  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542166.689   ± 3842.111  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     551547.973   ± 3747.676  ops/s
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
