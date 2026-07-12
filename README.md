# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-12T06:31:01Z
- **Commit:** [`79a5990`](https://github.com/dhoard/client_java/commit/79a5990fbde8597023bb40a07e9f77e32b19fdd1)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.86K | ± 283.68 | ops/s | **fastest** |
| prometheusNoLabelsInc | 54.78K | ± 2.14K | ops/s | 1.2x slower |
| prometheusAdd | 51.22K | ± 439.27 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.47K | ± 2.08K | ops/s | 1.4x slower |
| simpleclientInc | 6.53K | ± 39.10 | ops/s | 10x slower |
| simpleclientAdd | 6.32K | ± 283.37 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.28K | ± 88.29 | ops/s | 10x slower |
| openTelemetryAdd | 3.35K | ± 153.35 | ops/s | 20x slower |
| openTelemetryIncNoLabels | 3.31K | ± 299.59 | ops/s | 20x slower |
| openTelemetryInc | 3.06K | ± 148.03 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.05K | ± 1.07K | ops/s | **fastest** |
| simpleclient | 4.36K | ± 68.35 | ops/s | 1.4x slower |
| prometheusNative | 2.58K | ± 64.44 | ops/s | 2.3x slower |
| openTelemetryClassic | 766.53 | ± 23.09 | ops/s | 7.9x slower |
| openTelemetryExponential | 662.87 | ± 45.12 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.20K | ± 1.25K | ops/s | **fastest** |
| openMetricsWriteToNull | 23.67K | ± 1.62K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 498.52K | ± 4.68K | ops/s | **fastest** |
| prometheusWriteToByteArray | 493.12K | ± 2.70K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.36K | ± 1.96K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.02K | ± 4.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48470.349   ± 2082.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3346.369    ± 153.345  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3064.547    ± 148.032  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3314.241    ± 299.585  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51215.428    ± 439.268  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65859.880    ± 283.677  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      54779.876   ± 2141.280  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6324.087    ± 283.366  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6528.028     ± 39.098  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6280.089     ± 88.286  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        766.529     ± 23.086  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        662.867     ± 45.124  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6049.086   ± 1070.070  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2583.438     ± 64.442  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4359.739     ± 68.348  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23672.838   ± 1622.535  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24198.522   ± 1245.469  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471016.579   ± 4855.003  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479358.240   ± 1955.076  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     493118.620   ± 2702.965  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     498524.277   ± 4675.832  ops/s
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
