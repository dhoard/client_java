# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-30T06:10:29Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 59.80K | ± 1.32K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.46K | ± 899.40 | ops/s | 1.2x slower |
| prometheusAdd | 48.41K | ± 98.55 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 40.19K | ± 4.02K | ops/s | 1.5x slower |
| simpleclientInc | 6.17K | ± 125.14 | ops/s | 9.7x slower |
| simpleclientAdd | 6.08K | ± 11.67 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 5.90K | ± 5.50 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.76K | ± 1.35K | ops/s | 13x slower |
| openTelemetryAdd | 4.01K | ± 928.94 | ops/s | 15x slower |
| openTelemetryInc | 3.75K | ± 254.96 | ops/s | 16x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 14.50K | ± 59.55 | ops/s | **fastest** |
| prometheusClassic | 7.56K | ± 84.01 | ops/s | 1.9x slower |
| prometheusClassicSingleThread | 5.94K | ± 7.45 | ops/s | 2.4x slower |
| simpleclient | 4.51K | ± 40.87 | ops/s | 3.2x slower |
| prometheusNative | 3.01K | ± 233.12 | ops/s | 4.8x slower |
| openTelemetryClassic | 729.08 | ± 39.42 | ops/s | 20x slower |
| openTelemetryExponential | 586.50 | ± 54.97 | ops/s | 25x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 27.50K | ± 476.05 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.25K | ± 2.14K | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 577.37K | ± 6.29K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.42K | ± 5.25K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 546.73K | ± 1.92K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 538.95K | ± 3.92K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      40189.109   ± 4016.194  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4009.867    ± 928.936  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3753.771    ± 254.965  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4759.165   ± 1348.945  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48407.352     ± 98.550  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59798.936   ± 1324.627  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51455.939    ± 899.396  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6079.616     ± 11.667  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6167.008    ± 125.140  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5899.150      ± 5.504  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        729.085     ± 39.422  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        586.500     ± 54.973  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7561.374     ± 84.013  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14501.222     ± 59.547  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       5937.696      ± 7.450  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3008.493    ± 233.120  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4505.209     ± 40.871  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26253.847   ± 2138.255  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27503.271    ± 476.054  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     538953.600   ± 3924.057  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     546731.226   ± 1916.239  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572422.515   ± 5246.518  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     577365.365   ± 6289.645  ops/s
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
