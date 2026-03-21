# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-21T05:10:27Z
- **Commit:** [`ce5867b`](https://github.com/dhoard/client_java/commit/ce5867b3e25e10c68a6face275732b994a80ec98)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.65K | ± 972.76 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.36K | ± 732.65 | ops/s | 1.2x slower |
| prometheusAdd | 51.61K | ± 148.38 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.66K | ± 604.61 | ops/s | 1.3x slower |
| simpleclientInc | 6.78K | ± 23.24 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.47K | ± 201.07 | ops/s | 10x slower |
| simpleclientAdd | 6.18K | ± 68.26 | ops/s | 11x slower |
| openTelemetryAdd | 1.61K | ± 200.82 | ops/s | 41x slower |
| openTelemetryInc | 1.34K | ± 189.76 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.21K | ± 91.66 | ops/s | 54x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.70K | ± 1.74K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 41.87 | ops/s | 1.7x slower |
| prometheusNative | 3.00K | ± 360.52 | ops/s | 2.6x slower |
| openTelemetryClassic | 685.97 | ± 53.08 | ops/s | 11x slower |
| openTelemetryExponential | 539.03 | ± 40.96 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 492.29K | ± 1.86K | ops/s | **fastest** |
| prometheusWriteToByteArray | 491.90K | ± 3.84K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.21K | ± 2.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 481.56K | ± 2.92K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50659.080    ± 604.606  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1611.705    ± 200.823  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1335.707    ± 189.761  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1206.885     ± 91.657  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51605.812    ± 148.384  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65650.526    ± 972.764  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56356.624    ± 732.651  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6182.410     ± 68.261  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6784.424     ± 23.236  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6470.026    ± 201.067  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        685.971     ± 53.076  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        539.026     ± 40.965  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7696.698   ± 1738.644  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2998.622    ± 360.523  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4510.024     ± 41.871  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     481564.967   ± 2918.116  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488208.215   ± 2456.811  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     491901.601   ± 3835.912  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     492293.669   ± 1862.706  ops/s
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
