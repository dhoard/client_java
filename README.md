# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-11-20T11:15:54Z
- **Commit:** [`3ea508f`](https://github.com/dhoard/client_java/commit/3ea508f61ddaa1f8b43266e3bf378d7f60e14f25)
- **JDK:** 25.0.5 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 7.0.0-1019-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 680.45M | ± 1494.69K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 370.47M | ± 407.89K | ops/s |
| prometheusLabelValuesInc | 138.74M | ± 4624.38K | ops/s |
| prometheusLabelValuesIncSingleThread | 68.33M | ± 112.39K | ops/s |
| prometheusInc | 77.10K | ± 130.45 | ops/s |
| prometheusNoLabelsInc | 65.72K | ± 817.38 | ops/s |
| prometheusAdd | 61.32K | ± 821.98 | ops/s |
| codahaleIncNoLabels | 56.74K | ± 181.75 | ops/s |
| openTelemetryBoundInc | 44.84K | ± 84.35 | ops/s |
| openTelemetryBoundAdd | 39.06K | ± 538.28 | ops/s |
| openTelemetryInc | 27.46K | ± 353.58 | ops/s |
| openTelemetryIncNoLabels | 27.11K | ± 230.71 | ops/s |
| openTelemetryAdd | 24.61K | ± 410.83 | ops/s |
| simpleclientInc | 7.80K | ± 79.44 | ops/s |
| simpleclientNoLabelsInc | 7.58K | ± 22.91 | ops/s |
| simpleclientAdd | 7.41K | ± 377.76 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.54K | ± 50.93 | ops/s |
| prometheusClassic | 8.56K | ± 1.48K | ops/s |
| prometheusClassicSingleThread | 7.20K | ± 22.49 | ops/s |
| openTelemetryClassic | 6.83K | ± 645.28 | ops/s |
| openTelemetryBoundClassic | 6.24K | ± 1.92K | ops/s |
| simpleclient | 5.87K | ± 89.05 | ops/s |
| prometheusNative | 3.67K | ± 300.27 | ops/s |
| openTelemetryBoundExponential | 903.82 | ± 18.97 | ops/s |
| openTelemetryExponential | 875.24 | ± 28.02 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 40.40K | ± 149.58 | ops/s |
| prometheusWriteToNull | 40.37K | ± 513.57 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 760.44K | ± 9.81K | ops/s |
| prometheusWriteToByteArray | 744.69K | ± 12.44K | ops/s |
| openMetricsWriteToNull | 713.83K | ± 17.55K | ops/s |
| openMetricsWriteToByteArray | 705.81K | ± 9.76K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.017 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.038 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.024 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.021 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.035 | — | — |
| CounterBenchmark.prometheusAdd | 0.060 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.048 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.056 | — | — |
| CounterBenchmark.simpleclientAdd | 0.128 | — | — |
| CounterBenchmark.simpleclientInc | 0.121 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.124 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.162 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.047 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.141 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.079 | — | — |
| HistogramBenchmark.prometheusClassic | 0.445 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.463 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.405 | — | — |
| HistogramBenchmark.prometheusNative | 417713.021 | — | — |
| HistogramBenchmark.simpleclient | 0.160 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.087 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.087 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18485.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18485.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56739.150    ± 181.750  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      24605.714    ± 410.834  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      39060.154    ± 538.275  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      44844.003     ± 84.349  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27464.672    ± 353.582  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      27107.889    ± 230.712  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61324.514    ± 821.983  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  680447002.299 ± 1494685.334  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  370468972.874 ± 407893.716  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      77099.659    ± 130.448  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  138735621.325 ± 4624377.025  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   68325548.629 ± 112385.319  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      65721.456    ± 817.385  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7406.288    ± 377.764  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7795.026     ± 79.442  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7577.004     ± 22.912  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6240.896   ± 1921.642  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        903.823     ± 18.968  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6829.590    ± 645.282  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        875.243     ± 28.019  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       8563.135   ± 1477.797  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17538.454     ± 50.926  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7199.579     ± 22.495  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3665.706    ± 300.274  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5874.530     ± 89.053  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      40403.525    ± 149.582  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      40373.265    ± 513.568  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     705812.058   ± 9760.106  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     713828.907  ± 17550.591  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     744688.708  ± 12439.989  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     760435.861   ± 9814.681  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
