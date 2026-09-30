# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-30T09:01:56Z
- **Commit:** [`39a91dd`](https://github.com/dhoard/client_java/commit/39a91ddb316ebbeebb8740a436109f9b9cca7e17)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 77.93K | ± 1.04K | ops/s |
| prometheusNoLabelsInc | 66.82K | ± 972.98 | ops/s |
| prometheusAdd | 61.44K | ± 525.33 | ops/s |
| codahaleIncNoLabels | 56.84K | ± 488.41 | ops/s |
| openTelemetryIncNoLabels | 22.13K | ± 24.59 | ops/s |
| openTelemetryInc | 18.06K | ± 438.44 | ops/s |
| openTelemetryAdd | 15.62K | ± 168.32 | ops/s |
| simpleclientInc | 7.90K | ± 81.95 | ops/s |
| simpleclientNoLabelsInc | 7.76K | ± 288.65 | ops/s |
| simpleclientAdd | 7.51K | ± 11.60 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.84K | ± 159.08 | ops/s |
| prometheusClassic | 7.46K | ± 1.53K | ops/s |
| prometheusClassicSingleThread | 6.81K | ± 1.07K | ops/s |
| simpleclient | 5.66K | ± 128.43 | ops/s |
| prometheusNative | 3.57K | ± 130.29 | ops/s |
| openTelemetryClassic | 1.08K | ± 9.80 | ops/s |
| openTelemetryExponential | 903.51 | ± 16.94 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.46K | ± 303.99 | ops/s |
| openMetricsWriteToNull | 34.14K | ± 873.77 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 682.53K | ± 6.66K | ops/s |
| prometheusWriteToByteArray | 669.10K | ± 8.48K | ops/s |
| openMetricsWriteToNull | 651.65K | ± 8.08K | ops/s |
| openMetricsWriteToByteArray | 649.46K | ± 9.39K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56841.656    ± 488.412  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15622.575    ± 168.324  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18057.650    ± 438.437  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22131.128     ± 24.591  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61435.951    ± 525.335  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77925.320   ± 1038.246  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66823.524    ± 972.981  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7514.812     ± 11.604  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7900.598     ± 81.954  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7760.448    ± 288.652  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1078.387      ± 9.795  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        903.514     ± 16.940  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7457.136   ± 1532.316  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17840.756    ± 159.080  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       6807.902   ± 1066.165  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3570.844    ± 130.286  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5661.568    ± 128.428  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34140.568    ± 873.773  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35458.955    ± 303.992  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     649455.306   ± 9389.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     651645.359   ± 8078.561  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     669104.341   ± 8476.981  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     682527.557   ± 6655.242  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
