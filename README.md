# Redis Client
- Redis Client Utilities, support 2 libraries [redigo/redis](https://github.com/gomodule/redigo) and [redis/go-redis](https://github.com/redis/go-redis) (v6, v8, v9)
- Redis Health Check
- Implement CacheAdapter (Memory Cache), which is the implementation of the below interface:
```go
package cache

import (
  "context"
  "time"
)

type CachePort interface {
  Get(ctx context.Context, key string) (string, error)
  GetMany(ctx context.Context, keys []string) (map[string]string, []string, error)
  ContainsKey(ctx context.Context, key string) (bool, error)
  Put(ctx context.Context, key string, value interface{}, expire time.Duration) error
  Expire(ctx context.Context, key string, expire time.Duration) (bool, error)
  Remove(ctx context.Context, key string) (bool, error)
  Clear(ctx context.Context) error
  Count(ctx context.Context) (int64, error)
  Keys(ctx context.Context) ([]string, error)
  Size(ctx context.Context) (int64, error)
  Close(ctx context.Context) error
}
```
- Implement RedisAdapter, which is the implementation of the above interface
#### Sample
- Sample is at [project-samples/go-admin](https://github.com/project-samples/go-admin)
## Installation
Please make sure to initialize a Go module before installing core-go/redis:

```shell
go get -u github.com/core-go/redis
```

Import:
```go
import "github.com/core-go/redis"
```
