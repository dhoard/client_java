# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-18T05:38:06Z
- **Commit:** [`4b69f40`](https://github.com/dhoard/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.00K | ± 254.87 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.90K | ± 407.29 | ops/s | 1.2x slower |
| prometheusAdd | 50.96K | ± 715.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.75K | ± 1.96K | ops/s | 1.4x slower |
| simpleclientInc | 6.54K | ± 154.49 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.44K | ± 266.75 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 307.06 | ops/s | 11x slower |
| openTelemetryAdd | 1.46K | ± 273.56 | ops/s | 45x slower |
| openTelemetryInc | 1.41K | ± 232.48 | ops/s | 47x slower |
| openTelemetryIncNoLabels | 1.30K | ± 185.16 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.73K | ± 2.39K | ops/s | **fastest** |
| simpleclient | 4.41K | ± 35.94 | ops/s | 1.3x slower |
| prometheusNative | 2.99K | ± 272.21 | ops/s | 1.9x slower |
| openTelemetryClassic | 674.22 | ± 7.39 | ops/s | 8.5x slower |
| openTelemetryExponential | 594.14 | ± 15.70 | ops/s | 9.6x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 470.34K | ± 6.44K | ops/s | **fastest** |
| openMetricsWriteToNull | 460.40K | ± 3.22K | ops/s | 1.0x slower |
| prometheusWriteToByteArray | 459.16K | ± 7.65K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 447.72K | ± 5.70K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48748.146   ± 1960.448  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1459.418    ± 273.555  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1407.650    ± 232.478  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1302.782    ± 185.160  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50955.099    ± 715.780  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66000.041    ± 254.867  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56896.341    ± 407.289  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6066.998    ± 307.062  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6544.661    ± 154.490  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6435.351    ± 266.746  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        674.223      ± 7.394  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        594.143     ± 15.703  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5731.677   ± 2394.866  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2986.062    ± 272.208  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4414.406     ± 35.937  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     447720.971   ± 5696.234  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     460400.435   ± 3222.563  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     459161.126   ± 7647.950  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     470342.844   ± 6436.702  ops/s
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
