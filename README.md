# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-27T13:31:22Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 77.82K | ± 1.42K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.24K | ± 706.76 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 57.37K | ± 755.09 | ops/s | 1.4x slower |
| prometheusAdd | 47.68K | ± 15.85K | ops/s | 1.6x slower |
| openTelemetryIncNoLabels | 22.16K | ± 128.84 | ops/s | 3.5x slower |
| openTelemetryInc | 18.18K | ± 467.12 | ops/s | 4.3x slower |
| openTelemetryAdd | 15.57K | ± 274.47 | ops/s | 5.0x slower |
| simpleclientInc | 7.80K | ± 97.94 | ops/s | 10.0x slower |
| simpleclientNoLabelsInc | 7.59K | ± 83.78 | ops/s | 10x slower |
| simpleclientAdd | 7.25K | ± 487.52 | ops/s | 11x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 17.82K | ± 90.11 | ops/s | **fastest** |
| prometheusClassicSingleThread | 7.50K | ± 20.09 | ops/s | 2.4x slower |
| simpleclient | 5.58K | ± 169.62 | ops/s | 3.2x slower |
| prometheusClassic | 5.16K | ± 321.74 | ops/s | 3.5x slower |
| prometheusNative | 3.94K | ± 282.16 | ops/s | 4.5x slower |
| openTelemetryClassic | 1.06K | ± 61.79 | ops/s | 17x slower |
| openTelemetryExponential | 890.41 | ± 28.42 | ops/s | 20x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.60K | ± 320.04 | ops/s | **fastest** |
| openMetricsWriteToNull | 34.53K | ± 908.68 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 703.65K | ± 2.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 686.10K | ± 7.68K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 657.26K | ± 7.72K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 645.10K | ± 6.54K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      57371.416    ± 755.093  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15565.002    ± 274.473  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18177.868    ± 467.120  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22160.217    ± 128.845  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47679.581  ± 15849.838  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77824.548   ± 1422.034  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67237.400    ± 706.762  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7253.801    ± 487.525  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7799.545     ± 97.942  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7587.283     ± 83.779  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1063.990     ± 61.793  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        890.413     ± 28.424  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5162.611    ± 321.736  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17816.930     ± 90.112  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7502.182     ± 20.088  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3944.147    ± 282.159  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5576.680    ± 169.617  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34530.683    ± 908.683  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35601.838    ± 320.038  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     645101.798   ± 6535.702  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     657259.471   ± 7718.124  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     686096.340   ± 7684.038  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     703652.823   ± 2452.391  ops/s
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
