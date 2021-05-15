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

## Example for Redis Client
```go
package main

import (
	"fmt"
	client "github.com/core-go/redis"
)

type User struct {
	FirstName string `json:"firstName,omitempty"`
	LastName  string `json:"lastName,omitempty"`
}

func main() {
	user := User{
		FirstName: "Peter",
		LastName:  "Parker",
	}
	redisUrl := "redis://@localhost:6379"
	redis, _ := client.NewRedisClient(redisUrl)
	//Does not Set Time To Live
	client.Set(redis, "user", user, 0)
	v, _ := client.Get(redis, "user")
	//Output will be 'user:  {"firstName":"Peter","lastName":"Parker"}'
	fmt.Println("user: ", v)
}
```

## Example for Redis Service
```go
package main

import (
	"fmt"
	"github.com/core-go/cache"
	"github.com/core-go/redis"
	"time"
)

type User struct {
	FirstName string `json:"firstName,omitempty"`
	LastName  string `json:"lastName,omitempty"`
	Email     string `json:"email,omitempty"`
}

func main() {
	user := User{
		FirstName: "Peter",
		LastName:  "Parker",
		Email:     "peter.parker@gmail.com",
	}

	//Example for RedisService
	redisService, _ := redis.NewRedisService("redis://localhost:6379")
	redisService.Put("user", &user, 0)

	redisData, _ := redisService.Get("user")
	fmt.Println("user in redis: ", redisData)

	//Example for MemoryCacheService
	cacheConfig := cache.CacheConfig{
		Size: 10*1024*1024,
		CleaningEnable: true,
		CleaningInterval: 10 * time.Minute}
	cacheService, _ := cache.NewMemoryCacheService(cacheConfig)
	cacheService.Put("user", &user, 10 * time.Hour)

	data, _ := cacheService.Get("user")
	fmt.Println("user in cache: ", data)
}
```