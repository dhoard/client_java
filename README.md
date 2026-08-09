# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-09T04:48:49Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 64.22K | ± 1.31K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.96K | ± 448.58 | ops/s | 1.1x slower |
| prometheusAdd | 51.06K | ± 581.29 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.27K | ± 1.11K | ops/s | 1.3x slower |
| openTelemetryIncNoLabels | 18.69K | ± 198.19 | ops/s | 3.4x slower |
| openTelemetryInc | 14.75K | ± 302.62 | ops/s | 4.4x slower |
| openTelemetryAdd | 12.89K | ± 133.48 | ops/s | 5.0x slower |
| simpleclientInc | 6.59K | ± 7.42 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.51K | ± 127.20 | ops/s | 9.9x slower |
| simpleclientAdd | 6.44K | ± 18.11 | ops/s | 10.0x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 12.31K | ± 31.54 | ops/s | **fastest** |
| prometheusClassic | 6.58K | ± 1.37K | ops/s | 1.9x slower |
| prometheusClassicSingleThread | 4.59K | ± 34.80 | ops/s | 2.7x slower |
| simpleclient | 4.36K | ± 22.55 | ops/s | 2.8x slower |
| prometheusNative | 2.76K | ± 394.94 | ops/s | 4.5x slower |
| openTelemetryExponential | 839.81 | ± 133.15 | ops/s | 15x slower |
| openTelemetryClassic | 819.14 | ± 70.14 | ops/s | 15x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 24.02K | ± 413.73 | ops/s | **fastest** |
| openMetricsWriteToNull | 24.00K | ± 218.89 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 496.13K | ± 8.16K | ops/s | **fastest** |
| prometheusWriteToByteArray | 494.85K | ± 1.80K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.74K | ± 2.36K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 475.06K | ± 4.25K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50267.197   ± 1105.870  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      12892.797    ± 133.480  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      14749.054    ± 302.615  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      18692.119    ± 198.188  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51061.800    ± 581.286  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64215.498   ± 1309.614  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56955.805    ± 448.577  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6436.944     ± 18.112  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6587.494      ± 7.424  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6510.855    ± 127.201  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        819.137     ± 70.139  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        839.811    ± 133.154  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6583.445   ± 1365.906  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12307.683     ± 31.539  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4585.004     ± 34.804  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2759.193    ± 394.935  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4355.293     ± 22.554  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23997.468    ± 218.888  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24019.858    ± 413.731  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     475061.282   ± 4250.429  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476737.654   ± 2361.730  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494846.806   ± 1799.889  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     496134.758   ± 8158.812  ops/s
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
