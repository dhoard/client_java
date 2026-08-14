# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-14T05:19:40Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 66.27K | ± 712.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.47K | ± 1.08K | ops/s | 1.2x slower |
| prometheusAdd | 50.83K | ± 535.44 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.88K | ± 432.09 | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.70K | ± 203.62 | ops/s | 3.5x slower |
| openTelemetryInc | 15.12K | ± 299.29 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.89K | ± 245.25 | ops/s | 5.1x slower |
| simpleclientInc | 6.63K | ± 52.44 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.35K | ± 54.96 | ops/s | 10x slower |
| simpleclientAdd | 6.13K | ± 252.58 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.32K | ± 25.56 | ops/s | **fastest** |
| prometheusClassic | 6.65K | ± 1.24K | ops/s | 1.9x slower |
| prometheusClassicSingleThread | 4.56K | ± 16.77 | ops/s | 2.7x slower |
| simpleclient | 4.47K | ± 48.78 | ops/s | 2.8x slower |
| prometheusNative | 3.18K | ± 80.55 | ops/s | 3.9x slower |
| openTelemetryExponential | 896.12 | ± 20.45 | ops/s | 14x slower |
| openTelemetryClassic | 873.60 | ± 89.42 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 24.10K | ± 254.98 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.62K | ± 480.13 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 507.93K | ± 8.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.46K | ± 6.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.61K | ± 2.87K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 485.67K | ± 4.66K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49875.106    ± 432.090  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12893.485    ± 245.254  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      15118.542    ± 299.287  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18696.499    ± 203.615  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50830.054    ± 535.438  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66273.526    ± 712.676  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56474.059   ± 1083.675  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6128.322    ± 252.584  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6625.525     ± 52.445  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6348.775     ± 54.955  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        873.604     ± 89.415  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        896.125     ± 20.455  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6647.611   ± 1241.504  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12316.580     ± 25.556  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4563.756     ± 16.775  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3182.867     ± 80.555  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4472.829     ± 48.784  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23617.069    ± 480.133  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24102.827    ± 254.981  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485669.035   ± 4656.601  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488610.288   ± 2867.336  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506455.362   ± 6319.391  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     507932.910   ± 8577.518  ops/s
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
