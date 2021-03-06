# freedns-go

Optimized DNS Server for Chinese users.

freedns-go tries to dispatch the request to a DNS upstream located in china, which is fast but maybe poisoned. If it detected any non-Chinese websites, it fallbacks to dispatch the request to the upstream which is trustable.

The cache policy is lazy cache. If there are some records are expired but in the cache, it will return the cached records and update it asynchronously.

## Usage

You can download the prebuilt binary from the [releases](https://github.com/Chenyao2333/freedns-go/releases) page. Use `-f 114.114.114.114:53` to set the upstream in China, and use `-c 8.8.8.8:53` to set the upstream which is trustable.

```
sudo ./freedns-go -f 114.114.114.114:53 -c 8.8.8.8:53 -l 0.0.0.0:53
```

Issue a request to the server just started:

```
host baidu.com 127.0.0.1
host google.com 127.0.0.1
```

You can see `baidu.com` is dispatched to `114.114.114.114`, but `google.com` is dispatched to `8.8.8.8` since it's not located in China.

![](https://pppublic.oss-cn-beijing.aliyuncs.com/pics/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202018-05-08%20%E4%B8%8B%E5%8D%889.49.36.png)

**Note: freedns-go just dispatches your queries to the optimal upstreams. Your network should be able to reach those upstreams (e.g. 8.8.8.8). You can do that by port forwarding, or any ways you like..**
