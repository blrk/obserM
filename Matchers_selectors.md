### How to apply matchers and selectors
* http_response_size_bytes: The base name of the metric, indicating it is tracking the size of HTTP responses in bytes.
* _bucket: The suffix _bucket indicates that this is a histogram bucket.
* 
```bash
prometheus_http_response_size_bytes_bucket{handler="/static/*filepath"}
```
* handler: A label that typically represents the route or handler in your web application that processed the HTTP request.
* /static/*filepath: The value of the handler label, which indicates that the metric is tracking requests to a path that serves static files. The *filepath part is a wildcard, meaning it can match any file path under the /static/ directory.
```bash
prometheus_http_response_size_bytes_bucket{handler="/static/"}
```
* Will not show any results
```bash
prometheus_http_response_size_bytes_bucket{handler=~"/static/"}
```
* Will not show any results
```bash
prometheus_http_response_size_bytes_bucket{handler=~"/static/*.*"}
```
* You get some response
```bash
prometheus_http_response_size_bytes_bucket{handler=~"/static/*.*", le="1000"}
```
* le stands for "less than or equal to."
* This part of the metric indicates that you're interested in responses that are 1000 bytes or smaller.
