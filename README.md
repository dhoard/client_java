# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-04T06:17:53Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 62.83K | ± 3.63K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.77K | ± 488.61 | ops/s | 1.1x slower |
| codahaleIncNoLabels | 50.91K | ± 673.86 | ops/s | 1.2x slower |
| prometheusAdd | 49.66K | ± 2.08K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.51K | ± 89.41 | ops/s | 3.4x slower |
| openTelemetryInc | 14.52K | ± 1.33K | ops/s | 4.3x slower |
| openTelemetryAdd | 11.83K | ± 1.59K | ops/s | 5.3x slower |
| simpleclientInc | 6.56K | ± 37.65 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.35K | ± 9.32 | ops/s | 9.9x slower |
| simpleclientAdd | 6.00K | ± 348.53 | ops/s | 10x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.21K | ± 158.84 | ops/s | **fastest** |
| prometheusClassic | 5.38K | ± 1.47K | ops/s | 2.3x slower |
| prometheusClassicSingleThread | 4.58K | ± 33.84 | ops/s | 2.7x slower |
| simpleclient | 4.43K | ± 59.19 | ops/s | 2.8x slower |
| prometheusNative | 2.96K | ± 269.92 | ops/s | 4.1x slower |
| openTelemetryExponential | 881.72 | ± 127.87 | ops/s | 14x slower |
| openTelemetryClassic | 766.86 | ± 13.43 | ops/s | 16x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| openMetricsWriteToNull | 23.87K | ± 461.25 | ops/s | **fastest** |
| prometheusWriteToNull | 23.27K | ± 339.71 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 504.26K | ± 7.55K | ops/s | **fastest** |
| openMetricsWriteToByteArray | 485.67K | ± 2.41K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 481.64K | ± 35.32K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 438.81K | ± 49.57K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50908.820    ± 673.860  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11830.449   ± 1585.941  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14520.654   ± 1334.090  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18513.119     ± 89.411  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      49658.976   ± 2077.356  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      62834.761   ± 3627.351  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56772.153    ± 488.606  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5996.703    ± 348.527  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6557.996     ± 37.654  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6346.821      ± 9.323  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        766.862     ± 13.425  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        881.721    ± 127.874  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5383.707   ± 1469.578  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12214.139    ± 158.843  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4578.650     ± 33.837  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2959.347    ± 269.917  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4432.693     ± 59.195  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23871.368    ± 461.253  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23267.234    ± 339.713  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     485666.467   ± 2413.544  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     438810.498  ± 49570.481  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481643.654  ± 35318.445  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     504257.534   ± 7546.566  ops/s
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
