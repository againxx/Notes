# Bazel Debug Log

## 背景
构建缓存没有命中？
构建特别慢？
构建缓存命中率低？
构建过程中都发生了啥？

## execution_log_json_file
### 使用方式
在构建命令中加入如 --execution_log_json_file=exec.log，构建完成后会打印出exec.log日志
execution log记录了构建过程中的所有的Action，对应的command，input文件，输出文件，是否是cacheable等。
### 使用场景
1. 构建的远程缓存命中率比预计的要低，可以通过查看Action的remoteCacheHit是否为true来判断是否命中缓存，以及cacheable是否为true来判断是否可以被缓存
2. 两台不同机器共享远程缓存，但是并没有按找预计中命中缓存，可以分别在两个机器上生成exection log，再diff两个日志的差别

## build_event_json_file
### 使用方式
在构建命令中加入如 --build_event_json_file=event.log，构建完成后会打印出event.log日志。
相比于execution_log_json_file，build_event_json_file可以给出构建过程中每个event更详细的配置信息
### 使用场景
如两台服务器的的execution log一致，同时cacheable为true，但是remoteCacheHit为false。这时有可能是加入了--noremote_accept_cached的选项，这时就需要用到event log来查看更具体的执行action的配置。
在optionList中查询option，如果有 "combinedForm":"--noremote_accept_cached" 就说明这个action不会查询缓存

## profile
### 使用方式
在构建命令中加入如 --profile=profile.log，构建完成后会打印出profile.log日志。
键入如下命令，可以生成构建时长的分析报告，查看各个action的构建时长占比。
```
bazel analyze-profile profile.log
```

### 使用场景
一般在构建时长比较长的时候，可以通过profile文件查看是否有特别长的构建任务，具体的任务内容还可以在chrome://tracing中打开profile文件。如下图中，可以看出耗时最长的是在platformclasspath.jar的action，同时已经命中缓存。如果是没有命中缓存的情况，可以示情况决定如何优化。

## 工具tools_remote
### 使用方式
github地址：https://github.com/bazelbuild/tools_remote
在bazel构建时加上--experimental_remote_grpc_log=grpc.log，构建完成后打印出grpc.log日志，但是需要tools_remote解析。

键入如下命令，可以得到bazel与远程服务器交互时的grpc请求与结果
```
bazel-bin/remote_client --grpc_log=grpc.log printlog
```

### 使用场景
这种方式得到的结果最清晰，如使用`bazel-bin/remote_client --grpc_log PATH_TO_LOG failed_actions`，可以把构建过程中远程调用失败的action都dump下来。
