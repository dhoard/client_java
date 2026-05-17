# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-17T06:56:38Z
- **Commit:** [`11cb921`](https://github.com/dhoard/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.35K | ± 531.83 | ops/s | **fastest** |
| prometheusNoLabelsInc | 50.95K | ± 36.12 | ops/s | 1.2x slower |
| prometheusAdd | 48.09K | ± 352.12 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.86K | ± 324.71 | ops/s | 1.4x slower |
| simpleclientInc | 6.17K | ± 52.55 | ops/s | 9.6x slower |
| simpleclientAdd | 6.02K | ± 175.09 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 5.79K | ± 150.44 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.07K | ± 390.91 | ops/s | 12x slower |
| openTelemetryInc | 4.44K | ± 476.64 | ops/s | 13x slower |
| openTelemetryAdd | 4.22K | ± 1.06K | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.65K | ± 884.62 | ops/s | **fastest** |
| simpleclient | 4.59K | ± 120.14 | ops/s | 1.0x slower |
| prometheusNative | 2.71K | ± 138.65 | ops/s | 1.7x slower |
| openTelemetryClassic | 724.01 | ± 25.90 | ops/s | 6.4x slower |
| openTelemetryExponential | 547.29 | ± 29.86 | ops/s | 8.5x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 27.27K | ± 149.31 | ops/s | **fastest** |
| prometheusWriteToNull | 27.19K | ± 384.19 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 558.78K | ± 7.65K | ops/s | **fastest** |
| prometheusWriteToByteArray | 552.74K | ± 6.85K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 526.71K | ± 3.56K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 513.59K | ± 4.66K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43864.176    ± 324.709  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4218.330   ± 1064.379  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4435.289    ± 476.642  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5068.324    ± 390.907  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48091.104    ± 352.118  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59354.987    ± 531.833  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      50945.396     ± 36.118  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6023.291    ± 175.088  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6168.149     ± 52.551  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5793.710    ± 150.440  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        724.010     ± 25.898  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        547.293     ± 29.856  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4652.101    ± 884.619  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2713.521    ± 138.648  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4588.370    ± 120.140  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27265.506    ± 149.315  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27189.896    ± 384.193  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     513588.174   ± 4657.221  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     526714.968   ± 3556.813  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     552738.838   ± 6853.189  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     558782.608   ± 7647.001  ops/s
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
