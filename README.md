## What latency is

### Networking (latency)

https://www.cloudflare.com/learning/performance/glossary/what-is-latency/

> Latency is the time it takes for data to pass from one point on a network to another.

(Yes this is the right definition of `networking latency`)

NOTE: According to this definition, the `time` output from `ping` command is not latency. 
In the following output, `time=35.2 ms`, which is `RTT` (round-trip time). It's pretty double of `latency` 
(aka, the latency in this case is about `35.2/2 ~ 17.6ms`. However, `RTT = 2 * latency` is not always true.

```
$ ping 1.1.1.1 -c 1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=49 time=35.2 ms
```

### Network latency from a Mozilla web performance article

https://developer.mozilla.org/en-US/docs/Web/Performance/Understanding_latency
(or https://web.archive.org/web/20240922180416/https://developer.mozilla.org/en-US/docs/Web/Performance/Understanding_latency)

> Network latency is the time it takes for a data request to get from
> the computer making the request, to the computer responding. Including
> the time it takes for a byte of data to make it from the responding
> computer back to the requesting computer.
> It is generally measured as a round trip delay.

### Jmeter

https://jmeter.apache.org/usermanual/glossary.html

> **Latency**. JMeter measures the latency from just before sending the
> request to just after the first response has been received.
> Thus the time includes all the processing needed to assemble the
> request as well as assembling the first part of the response,
> which in general will be longer than one byte. Protocol analysers
> (such as Wireshark) measure the time when bytes are actually
> sent/received over the interface. The JMeter time should be closer
> to that which is experienced by a browser or other application client.

### Nginx ingress controller (k8s or kubernetes)

In many log configurations, `latency` is defined as below

```
"latency": "$upstream_response_time s"
```

See more with, for example https://www.google.com/search?q="latency"%3A+"%24upstream_response_time+s". 
`Elasticsearch` has an intergration documentation with this format 
https://web.archive.org/web/20240922181130/https://www.elastic.co/docs/current/integrations/nginx_ingress_controller

So what is `$upstream_response_time`? According to `nginx`'s documentation (https://nginx.org/en/docs/http/ngx_http_upstream_module.html#var_upstream_response_time)

> `$upstream_response_time`
>
> keeps time spent on receiving the response from the upstream server;
> the time is kept in seconds with millisecond resolution.
> Times of several responses are separated by commas and colons like addresses in the $upstream_addr variable. 

Their blogs gives more details (https://blog.nginx.org/blog/using-nginx-logging-for-application-performance-monitoring)

> `$request_time` – Full request time, starting when NGINX reads the first byte from the client and ending when NGINX sends the last byte of the response body
>
> `$upstream_connect_time` – Time spent establishing a connection with an upstream server
>
> `$upstream_header_time` – Time between establishing a connection to an upstream server and receiving the first byte of the response header
>
> `$upstream_response_time` – Time between establishing a connection to an upstream server and receiving the last byte of the response body

