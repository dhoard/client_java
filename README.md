# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-08-03T06:52:42Z
- **Commit:** [`922943c`](https://github.com/dhoard/client_java/commit/922943cfe12acb5e373a0a6152384673c3c7b6dc)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** Intel(R) Xeon(R) Platinum 8370C CPU @ 2.80GHz, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 31.51K | ± 22.54 | ops/s | **fastest** |
| prometheusNoLabelsInc | 30.55K | ± 1.18K | ops/s | 1.0x slower |
| codahaleIncNoLabels | 30.09K | ± 743.28 | ops/s | 1.0x slower |
| prometheusAdd | 28.40K | ± 383.20 | ops/s | 1.1x slower |
| openTelemetryIncNoLabels | 16.95K | ± 70.31 | ops/s | 1.9x slower |
| openTelemetryInc | 13.12K | ± 147.20 | ops/s | 2.4x slower |
| openTelemetryAdd | 11.55K | ± 71.96 | ops/s | 2.7x slower |
| simpleclientInc | 6.86K | ± 125.22 | ops/s | 4.6x slower |
| simpleclientNoLabelsInc | 6.65K | ± 10.62 | ops/s | 4.7x slower |
| simpleclientAdd | 6.28K | ± 229.06 | ops/s | 5.0x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusClassicPerThread | 7.70K | ± 197.34 | ops/s | **fastest** |
| simpleclient | 4.34K | ± 139.35 | ops/s | 1.8x slower |
| prometheusClassic | 3.75K | ± 1.99K | ops/s | 2.1x slower |
| prometheusClassicSingleThread | 3.26K | ± 101.20 | ops/s | 2.4x slower |
| prometheusNative | 2.36K | ± 231.71 | ops/s | 3.3x slower |
| openTelemetryClassic | 618.54 | ± 20.13 | ops/s | 12x slower |
| openTelemetryExponential | 558.93 | ± 17.09 | ops/s | 14x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 18.20K | ± 112.06 | ops/s | **fastest** |
| openMetricsWriteToNull | 18.19K | ± 102.18 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 318.95K | ± 2.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 315.23K | ± 2.26K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 296.23K | ± 2.47K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 293.33K | ± 3.18K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      30085.813    ± 743.283  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      11546.983     ± 71.964  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      13123.850    ± 147.195  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      16950.975     ± 70.306  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      28403.252    ± 383.200  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      31506.700     ± 22.538  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      30549.983   ± 1175.336  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6283.736    ± 229.061  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6856.112    ± 125.222  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6651.768     ± 10.619  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        618.537     ± 20.126  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.928     ± 17.088  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       3749.030   ± 1992.707  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       7696.377    ± 197.343  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       3264.697    ± 101.196  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2362.610    ± 231.711  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4342.991    ± 139.347  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      18191.912    ± 102.183  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      18202.335    ± 112.058  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     293328.875   ± 3175.309  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     296228.227   ± 2474.688  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     315234.861   ± 2257.562  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     318947.509   ± 2417.798  ops/s
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
