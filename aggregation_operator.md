### How to use Aggregation operator
```bash
node_cpu_seconds_total
```
* node: Refers to the host machine (node) where the metric is being collected.
* cpu: Indicates that this metric is related to CPU usage.
* seconds_total: Represents the total time, in seconds, that the CPU has spent in various modes (e.g., idle, user, system).
```bash
sum(node_cpu_seconds_total)
```
```bash
sum(node_cpu_seconds_total) by (mode)
```
```bash
{mode="idle"} 769.97
{mode="iowait"} 0.27999999999999997
{mode="irq"} 0
{mode="nice"} 0.060000000000000005
{mode="softirq"} 0.03
{mode="steal"} 0.24
{mode="system"} 5.45
{mode="user"} 35.17
```
```bash
sum(node_cpu_seconds_total) without (mode)
```
```bash
{cpu="0", instance="192.168.122.168:9100", job="docker server"} 599.92
{cpu="1", instance="192.168.122.168:9100", job="docker server"} 599.94
```
```bash
topk(3, sum(node_cpu_seconds_total) by (mode))
```
```bash
{mode="idle"} 1397.54
{mode="user"} 35.28
{mode="system"} 5.8100000000000005
```
```bash
bottomk(3, sum(node_cpu_seconds_total) by (mode))
```
```bash
{mode="irq"} 0
{mode="nice"} 0.060000000000000005
{mode="softirq"} 0.11
```
```bash
group(node_cpu_seconds_total) 
```
```bash
{} 1
```
```bash
group(node_cpu_seconds_total) by (mode)
```
```bash
{mode="idle"} 1
{mode="iowait"} 1
{mode="irq"} 1
{mode="nice"} 1
{mode="softirq"} 1
{mode="steal"} 1
{mode="system"} 1
{mode="user"} 1
```
```bash
avg(node_cpu_seconds_total) by (mode)
```
```bash
{mode="idle"} 1072.135
{mode="iowait"} 0.155
{mode="irq"} 0
{mode="nice"} 0.03
{mode="softirq"} 0.095
{mode="steal"} 0.18000000000000002
{mode="system"} 3.1100000000000003
{mode="user"} 18.195
```
```bash
topk(3, avg(node_cpu_seconds_total) by (mode))
```
```bash
{mode="idle"} 1236.415
{mode="user"} 18.409999999999997
{mode="system"} 3.19
```