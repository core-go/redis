# Redis Client
- Redis Client Utilities
- Redis Service: is an implementation of CacheService of [core-go/cache](https://github.com/core-go/cache)

## Installation
Please make sure to initialize a Go module before installing core-go/redis:

```shell
go get -u github.com/core-go/redis
```

Import:
```go
import "github.com/core-go/redis"
```

## Version
redigo
```shell
module github.com/core-go/redis

go 1.11

require github.com/garyburd/redigo v1.6.2
```

redis v8
```shell
module github.com/core-go/redis

go 1.11

require github.com/go-redis/redis/v8 v8.11.4
```

redis v6
```shell
module github.com/core-go/redis

go 1.11

require github.com/go-redis/redis v6.15.9+incompatible
```