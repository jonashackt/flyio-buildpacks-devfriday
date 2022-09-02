# flyio-buildpacks-devfriday
Having a look at https://fly.io/


## HowTo

https://fly.io/docs/hands-on/install-flyctl/

### Install flyctl

On a Mac install flyctl via brew:

```shell
brew install flyctl
```


### Signup to fly.io

```shell
flyctl auth signup
```

![signup-to-flyio](screenshots/signup-to-flyio.png)


### Launch example Spring Boot app on fly.io

Let's use https://github.com/jonashackt/microservice-api-spring-boot

So check it out locally and run 

```
flyctl launch --image flyio/hellofly:latest
```



### error unable to calculate memory configuration

```shell
2022-09-02T09:39:21Z   [info]Calculating JVM memory based on 448164K available memory
2022-09-02T09:39:21Z   [info]For more information on this calculation, see https://paketo.io/docs/reference/java-reference/#memory-calculator
2022-09-02T09:39:21Z   [info]unable to calculate memory configuration
2022-09-02T09:39:21Z   [info]fixed memory regions require 637219K which is greater than 448164K available for allocation: -XX:MaxDirectMemorySize=10M, -XX:MaxMetaspaceSize=125219K, -XX:ReservedCodeCacheSize=240M, -Xss1M * 250 threads
2022-09-02T09:39:21Z   [info]ERROR: failed to launch: exec.d: failed to execute exec.d file at path '/layers/paketo-buildpacks_bellsoft-liberica/helper/exec.d/memory-calculator': exit status 1
2022-09-02T09:39:21Z   [info]Starting clean up.
--> v2 failed - Failed due to unhealthy allocations - no stable job version to auto revert to and deploying as v3
```

Fix [as stated here](https://community.fly.io/t/out-of-memory-restarts/1629/3): 

```shell
flyctl scale memory 1024
```