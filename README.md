# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-29T07:44:09Z
- **Commit:** [`2a2c73d`](https://github.com/dhoard/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.32K | ± 1.73K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.10K | ± 455.97 | ops/s | 1.1x slower |
| prometheusAdd | 51.28K | ± 199.14 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.87K | ± 1.10K | ops/s | 1.4x slower |
| simpleclientInc | 6.59K | ± 7.52 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.47K | ± 109.08 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 226.24 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.33K | ± 346.56 | ops/s | 20x slower |
| openTelemetryAdd | 3.14K | ± 153.99 | ops/s | 21x slower |
| openTelemetryInc | 2.95K | ± 55.48 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.61K | ± 727.94 | ops/s | **fastest** |
| simpleclient | 4.43K | ± 30.79 | ops/s | 1.0x slower |
| prometheusNative | 2.95K | ± 320.42 | ops/s | 1.6x slower |
| openTelemetryClassic | 761.55 | ± 20.08 | ops/s | 6.0x slower |
| openTelemetryExponential | 582.09 | ± 20.96 | ops/s | 7.9x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 23.29K | ± 449.84 | ops/s | **fastest** |
| prometheusWriteToNull | 23.25K | ± 894.08 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 510.95K | ± 2.95K | ops/s | **fastest** |
| prometheusWriteToByteArray | 506.20K | ± 2.92K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 490.62K | ± 3.06K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 479.57K | ± 7.50K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47870.259   ± 1098.840  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3140.758    ± 153.990  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2948.545     ± 55.475  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3327.120    ± 346.564  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51281.500    ± 199.141  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65317.046   ± 1729.554  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57097.641    ± 455.970  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6298.636    ± 226.245  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6591.462      ± 7.515  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6466.989    ± 109.076  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        761.552     ± 20.079  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        582.085     ± 20.964  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4606.967    ± 727.942  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2952.209    ± 320.416  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4427.216     ± 30.787  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23292.372    ± 449.840  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23248.821    ± 894.083  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     479567.157   ± 7501.835  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     490616.619   ± 3063.970  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     506202.971   ± 2920.416  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     510953.673   ± 2951.384  ops/s
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
