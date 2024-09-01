### How to use functions
#### absent() 
* function in Prometheus is used to determine whether a specific metric or time series is absent or missing at a given point in time. 
* Alerting: You can use the absent() function to trigger an alert if a metric is missing.
```bash
absent(node_cpu_seconds_total)
```
* Gives empty result
```bash
absent(node_cpu_seconds_total{cpu="x09d"})
```
```bash
absent(node_cpu_seconds_total{cpu="x09d"}[1h])
```
* Can't take range
#### absent_over_time() 
* function in Prometheus is used to determine whether a specific metric or time series has been absent
* Alerting on Persistent Metric Absence: You can use absent_over_time() to create alerts that trigger if a metric has been missing for a certain period of time. 
```bash
absent_over_time(node_cpu_seconds_total{cpu="x09d"}[1h])
```
```bash
{cpu="x09d"} 1
```
#### abs() 
* function in Prometheus is used to return the absolute value of each element in an instant vector. 
* The absolute value of a number is its non-negative value, so abs() effectively removes any negative signs from the values in the vector.

#### ceil() 
* function in Prometheus is used to round up the values in an instant vector to the nearest integer. 
* This means that any non-integer value in the vector will be rounded up to the smallest integer that is greater than or equal to that value.
* suppose 1.2, 2.7, and 3.0, are the result after applying ceil() would be 2, 3, and 3 respectively.

#### floor() 
* function in Prometheus is used to round down the values in an instant vector to the nearest integer. 
* This means that any non-integer value in the vector will be rounded down to the largest integer that is less than or equal to that value
* Suppose 1.8, 2.3, and 3.0, are the result after applying floor() would be 1, 2, and 3 respectively.

#### clamp_min() 
* function in Prometheus is used to limit the values in an instant vector to a specified minimum threshold. I
* If any value in the vector is below this threshold, clamp_min() will adjust it to the minimum threshold value. 
* Values that are already above the threshold remain unchanged.
```bash
clamp_min(node_cpu_seconds_total, 300)
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3386.91
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="irq"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="nice"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="steal"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="system"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="user"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3389.72
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="irq"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="nice"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="steal"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="system"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="user"} 300
```
```bash
clamp_max(node_cpu_seconds_total, 3500)
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3500
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 0.27
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="irq"} 0
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="nice"} 0.01
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 0.33
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="steal"} 0.4
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="system"} 4.26
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="user"} 21.32
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3500
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 0.08
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="irq"} 0
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="nice"} 0.05
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 0.4
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="steal"} 0.19
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="system"} 4.18
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="user"} 21.55
```
```bash
clamp(node_cpu_seconds_total, 300, 3500)
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3500
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="irq"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="nice"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="steal"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="system"} 300
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="user"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="idle"} 3500
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="irq"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="nice"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="steal"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="system"} 300
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="user"} 300
```
```bash
clamp(node_cpu_seconds_total offset 1h, 300, 3500)
```
```bash
avg_over_time(node_cpu_seconds_total [1h])
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="idle"} 11078.293958333334
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 1.2772083333333348
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="irq"} 0
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="nice"} 0.01
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 1.2590833333333329
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="steal"} 0.546458333333333
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="system"} 7.16554166666667
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="user"} 27.482374999999983
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="idle"} 11086.649500000005
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 0.13470833333333332
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="irq"} 0
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="nice"} 0.05
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 0.7248333333333334
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="steal"} 0.3513333333333333
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="system"} 6.794374999999998
{cpu="1", instance="192.168.122.168:9100", job="docker server", mode="user"} 28.226708333333345
```
```bash
avg_over_time(node_cpu_seconds_total{cpu="0"} [1h])
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="idle"} 11227.654916666672
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="iowait"} 1.2979583333333335
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="irq"} 0
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="nice"} 0.01
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="softirq"} 1.268791666666666
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="steal"} 0.5510416666666668
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="system"} 7.247916666666667
{cpu="0", instance="192.168.122.168:9100", job="docker server", mode="user"} 27.661833333333334
```
