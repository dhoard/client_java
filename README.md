# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-02T06:40:46Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 65.13K | ± 632.89 | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.50K | ± 3.55K | ops/s | 1.2x slower |
| prometheusAdd | 50.95K | ± 462.50 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.61K | ± 1.27K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 16.95K | ± 1.92K | ops/s | 3.8x slower |
| openTelemetryInc | 14.92K | ± 313.78 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.98K | ± 26.61 | ops/s | 5.0x slower |
| simpleclientInc | 6.53K | ± 33.47 | ops/s | 10.0x slower |
| simpleclientAdd | 6.44K | ± 22.47 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.31K | ± 55.50 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.28K | ± 21.56 | ops/s | **fastest** |
| prometheusClassic | 4.58K | ± 681.67 | ops/s | 2.7x slower |
| prometheusClassicSingleThread | 4.56K | ± 33.33 | ops/s | 2.7x slower |
| simpleclient | 4.41K | ± 87.08 | ops/s | 2.8x slower |
| prometheusNative | 2.89K | ± 244.41 | ops/s | 4.2x slower |
| openTelemetryExponential | 895.17 | ± 98.48 | ops/s | 14x slower |
| openTelemetryClassic | 773.70 | ± 6.21 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 23.77K | ± 354.45 | ops/s | **fastest** |
| openMetricsWriteToNull | 22.68K | ± 353.50 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 515.18K | ± 3.05K | ops/s | **fastest** |
| prometheusWriteToByteArray | 499.70K | ± 5.01K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.03K | ± 3.72K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 483.22K | ± 5.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48607.458   ± 1270.955  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12983.389     ± 26.611  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14921.670    ± 313.781  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16947.873   ± 1922.931  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50952.975    ± 462.504  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65126.994    ± 632.886  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54499.368   ± 3552.882  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6442.246     ± 22.471  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6530.727     ± 33.466  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6305.185     ± 55.504  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        773.705      ± 6.205  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        895.172     ± 98.479  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4580.902    ± 681.670  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12278.175     ± 21.564  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4564.451     ± 33.327  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2891.959    ± 244.411  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4408.698     ± 87.082  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      22678.673    ± 353.496  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23766.976    ± 354.446  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     483217.341   ± 5659.638  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490031.304   ± 3719.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     499697.196   ± 5013.948  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     515180.870   ± 3051.377  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval
- **Within run** compares benchmarks in the same result set, not against the base commit.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
