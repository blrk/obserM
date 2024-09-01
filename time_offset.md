### How to use tiem offset
```bash
prometheus_http_requests_total
```
```bash
prometheus_http_requests_total offset 10m
```
```bash
group(prometheus_http_requests_total) by (code)
```
```bash
{code="200"} 1
{code="302"} 1
{code="400"} 1
```
```bash
avg(prometheus_http_requests_total) by (code)
```
```bash
{code="200"} 5.980392156862745
{code="302"} 1
{code="400"} 8
```
```bash
avg(prometheus_http_requests_total offset 30m) by (code)
```
```bash
{code="200"} 3.0784313725490193
{code="302"} 1
{code="400"} 2
```