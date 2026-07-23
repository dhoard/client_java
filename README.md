# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-23T06:37:54Z
- **Commit:** [`0a91771`](https://github.com/dhoard/client_java/commit/0a917717bbd9ec2112f3e85b4d8d03777a39b511)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 71.95K | ± 4.52K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.29K | ± 1.30K | ops/s | 1.1x slower |
| prometheusAdd | 62.11K | ± 2.07K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.76K | ± 122.18 | ops/s | 1.3x slower |
| simpleclientInc | 7.96K | ± 73.66 | ops/s | 9.0x slower |
| simpleclientNoLabelsInc | 7.61K | ± 74.01 | ops/s | 9.4x slower |
| simpleclientAdd | 7.56K | ± 228.98 | ops/s | 9.5x slower |
| openTelemetryIncNoLabels | 5.70K | ± 1.65K | ops/s | 13x slower |
| openTelemetryInc | 5.67K | ± 1.68K | ops/s | 13x slower |
| openTelemetryAdd | 5.09K | ± 1.11K | ops/s | 14x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 18.88K | ± 38.33 | ops/s | **fastest** |
| prometheusClassic | 9.39K | ± 181.33 | ops/s | 2.0x slower |
| prometheusClassicSingleThread | 7.66K | ± 22.54 | ops/s | 2.5x slower |
| simpleclient | 5.91K | ± 54.98 | ops/s | 3.2x slower |
| prometheusNative | 3.75K | ± 285.95 | ops/s | 5.0x slower |
| openTelemetryClassic | 893.39 | ± 8.21 | ops/s | 21x slower |
| openTelemetryExponential | 711.45 | ± 38.23 | ops/s | 27x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 35.41K | ± 289.70 | ops/s | **fastest** |
| openMetricsWriteToNull | 35.40K | ± 200.77 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 700.87K | ± 11.58K | ops/s | **fastest** |
| prometheusWriteToByteArray | 684.89K | ± 3.88K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 663.89K | ± 3.49K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 641.06K | ± 4.76K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56755.258    ± 122.182  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5086.656   ± 1108.003  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5673.861   ± 1676.051  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5698.263   ± 1654.699  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      62107.444   ± 2070.279  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      71947.622   ± 4521.754  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67287.580   ± 1304.016  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7562.924    ± 228.982  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7962.791     ± 73.663  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7614.476     ± 74.011  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        893.389      ± 8.212  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        711.446     ± 38.233  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9391.388    ± 181.325  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      18881.535     ± 38.332  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7664.186     ± 22.541  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3751.137    ± 285.949  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5908.622     ± 54.984  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35403.646    ± 200.765  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35409.951    ± 289.700  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     641064.797   ± 4762.846  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     663886.933   ± 3486.558  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     684894.814   ± 3875.166  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     700867.542  ± 11575.750  ops/s
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
