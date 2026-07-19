# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-07-19T06:15:27Z
- **Commit:** [`8d91443`](https://github.com/dhoard/client_java/commit/8d91443665952d8a2585a9e2f220a5811ef2a051)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1020-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusInc | 68.29K | ± 703.12 | ops/s | **fastest** |
| prometheusNoLabelsInc | 66.26K | ± 878.57 | ops/s | 1.0x slower |
| codahaleIncNoLabels | 61.93K | ± 472.33 | ops/s | 1.1x slower |
| prometheusAdd | 56.77K | ± 565.24 | ops/s | 1.2x slower |
| simpleclientNoLabelsInc | 11.06K | ± 260.80 | ops/s | 6.2x slower |
| simpleclientAdd | 10.57K | ± 65.69 | ops/s | 6.5x slower |
| simpleclientInc | 10.27K | ± 456.58 | ops/s | 6.7x slower |
| openTelemetryIncNoLabels | 7.49K | ± 1.20K | ops/s | 9.1x slower |
| openTelemetryAdd | 5.40K | ± 649.29 | ops/s | 13x slower |
| openTelemetryInc | 5.19K | ± 195.63 | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| simpleclient | 7.01K | ± 155.37 | ops/s | **fastest** |
| prometheusClassic | 6.99K | ± 2.45K | ops/s | 1.0x slower |
| prometheusNative | 5.35K | ± 202.10 | ops/s | 1.3x slower |
| openTelemetryClassic | 906.59 | ± 17.77 | ops/s | 7.7x slower |
| openTelemetryExponential | 723.41 | ± 31.33 | ops/s | 9.7x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 33.97K | ± 151.00 | ops/s | **fastest** |
| openMetricsWriteToNull | 33.79K | ± 90.13 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | Within run |
|:----------|------:|------:|:------|:-----------|
| prometheusWriteToNull | 755.16K | ± 43.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 752.87K | ± 30.54K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 685.87K | ± 28.29K | ops/s | 1.1x slower |
| openMetricsWriteToNull | 684.47K | ± 12.00K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      61932.112    ± 472.335  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5401.337    ± 649.288  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       5192.604    ± 195.625  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7486.035   ± 1203.410  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56765.393    ± 565.240  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      68291.806    ± 703.121  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66263.648    ± 878.571  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10569.307     ± 65.685  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10267.589    ± 456.578  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11058.580    ± 260.800  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        906.588     ± 17.774  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        723.406     ± 31.326  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6985.841   ± 2453.562  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5351.659    ± 202.097  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7005.798    ± 155.365  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      33788.196     ± 90.130  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33972.750    ± 150.997  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     685865.977  ± 28290.153  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     684469.245  ± 12003.086  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     752867.034  ± 30537.642  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     755162.600  ± 43186.945  ops/s
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
