# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-16T05:28:51Z
- **Commit:** [`229e2e0`](https://github.com/dhoard/client_java/commit/229e2e003bd639f3744566940f503d05e8b9ba18)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 63.04K | ± 3.06K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.08K | ± 472.93 | ops/s | 1.1x slower |
| prometheusAdd | 51.70K | ± 125.47 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 48.49K | ± 1.51K | ops/s | 1.3x slower |
| simpleclientInc | 6.55K | ± 196.89 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.45K | ± 203.32 | ops/s | 9.8x slower |
| simpleclientAdd | 6.26K | ± 235.08 | ops/s | 10x slower |
| openTelemetryAdd | 1.46K | ± 244.56 | ops/s | 43x slower |
| openTelemetryInc | 1.43K | ± 139.42 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.23K | ± 7.87 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 1.42K | ops/s | **fastest** |
| simpleclient | 4.54K | ± 13.14 | ops/s | 1.2x slower |
| prometheusNative | 3.04K | ± 239.10 | ops/s | 1.8x slower |
| openTelemetryClassic | 683.40 | ± 23.70 | ops/s | 8.1x slower |
| openTelemetryExponential | 543.15 | ± 9.33 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 470.19K | ± 3.00K | ops/s | **fastest** |
| prometheusWriteToNull | 470.05K | ± 4.27K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 456.49K | ± 5.35K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 449.80K | ± 5.00K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48491.752   ± 1508.509  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1458.758    ± 244.555  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1431.447    ± 139.423  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1226.841      ± 7.870  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51699.314    ± 125.474  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      63040.864   ± 3061.112  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57082.218    ± 472.928  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6257.776    ± 235.075  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6545.490    ± 196.894  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6446.636    ± 203.319  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        683.395     ± 23.697  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        543.145      ± 9.334  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5527.970   ± 1420.064  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3040.842    ± 239.105  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4535.487     ± 13.144  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     449799.455   ± 4997.376  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     456485.606   ± 5354.703  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     470188.915   ± 3001.564  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     470045.287   ± 4267.543  ops/s
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
