# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-02T07:04:21Z
- **Commit:** [`0a88856`](https://github.com/dhoard/client_java/commit/0a888563c2b1d57fccee3a2537fa6348b7003724)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.54K | ± 2.10K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.37K | ± 385.94 | ops/s | 1.1x slower |
| prometheusAdd | 48.20K | ± 238.43 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.13K | ± 1.94K | ops/s | 1.4x slower |
| simpleclientInc | 6.19K | ± 121.75 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 5.85K | ± 43.21 | ops/s | 10x slower |
| simpleclientAdd | 5.70K | ± 444.17 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.56K | ± 1.43K | ops/s | 11x slower |
| openTelemetryAdd | 4.63K | ± 861.30 | ops/s | 13x slower |
| openTelemetryInc | 4.54K | ± 1.12K | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.86K | ± 1.84K | ops/s | **fastest** |
| simpleclient | 4.33K | ± 62.24 | ops/s | 1.4x slower |
| prometheusNative | 3.05K | ± 167.37 | ops/s | 1.9x slower |
| openTelemetryClassic | 752.37 | ± 26.59 | ops/s | 7.8x slower |
| openTelemetryExponential | 575.72 | ± 20.72 | ops/s | 10x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.58K | ± 266.53 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.14K | ± 408.78 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 555.27K | ± 1.54K | ops/s | **fastest** |
| prometheusWriteToNull | 553.26K | ± 11.04K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 530.25K | ± 1.99K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 514.24K | ± 5.43K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43132.572   ± 1936.533  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4629.399    ± 861.304  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4542.881   ± 1116.812  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5560.985   ± 1432.441  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48201.479    ± 238.433  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58541.654   ± 2103.464  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51365.219    ± 385.936  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5701.040    ± 444.174  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6192.066    ± 121.754  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5850.969     ± 43.207  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        752.371     ± 26.595  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        575.720     ± 20.724  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5855.104   ± 1838.201  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3053.687    ± 167.367  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4326.566     ± 62.243  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27143.296    ± 408.784  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27583.183    ± 266.528  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     514243.418   ± 5429.956  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     530247.571   ± 1993.095  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     555272.668   ± 1538.599  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     553262.862  ± 11042.547  ops/s
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
