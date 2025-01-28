# gpt 文章翻译器

本工程是一个调用兼容openai chat接口实现的翻译工具。

推荐使用deepseek api。

本工具支持中英翻译并润色。


## 快速开始

### 1. 安装环境与依赖库

1. 要求python3环境，推荐python3.11
2. 安装依赖库`pip install openai`


### 2. 配置调用的模型信息


创建openai api配置信息`env.json`:


```json
{
    "base_url":"https://api.deepseek.com/v1",
    "api_key":"sk-xxx",
    "model":"deepseek-chat"
}
```

注：上面是deepseek配置样例，把api_key换成自己在平台上创建的的api_key即可。

### 3. 运行翻译工具

#### 3.1 翻译参数内容

```sh
python translator.py "r-nacos是一个用rust实现的nacos服务。相较于java nacos来 说，是一个提供相同功能，启动更快、占用系统资源更小（初始内存小于10M）、性能更高、运行更稳定的服务。"

out:

翻译文本长度: 91
base_url: https://api.deepseek.com/v1 ,model: deepseek-chat
fromLang: 中文 ,toLang: 英文
------------------------------------------------------------
sub_translation text len: 91 ,time: 34.9991660118103
直译结果：

r-nacos is a nacos service implemented in rust. Compared to java nacos, it is a service that provides the same functions, starts faster, occupies less system resources (initial memory less than 10M), has higher performance, and runs more stably.

------------------------------------------------------------
润色结果：

r-nacos is a nacos service built using Rust. In comparison to the Java-based nacos, it offers identical functionalities but with faster startup times, lower system resource usage (initial memory under 10M), superior performance, and enhanced operational stability.
------------------------------------------------------------
translation,time consumed: 34.99927997589111

```

注：默认使用当前目录下的`env.json`配置文件，从中文翻译为英文；也可以通过配置参数指定，参数配置参考后面的参数说明。


#### 3.1 翻译文件

通过参数`-i inputfile` 和`-o outputfile`指定翻译原文件与翻译后写入的文件。


```sh
python translator.py -i xxx/docs/index.md -o out_xxx.md

exp out:

翻译文本长度: 4722
base_url: https://api.deepseek.com/v1 ,model: deepseek-chat
fromLang: 中文 ,toLang: 英文
------------------------------------------------------------
sub_translation text len: 2840 ,time: 515.0595738887787
sub_translation text len: 1389 ,time: 57.134907960891724
sub_translation text len: 493 ,time: 38.153035163879395
------------------------------------------------------------
translation,time consumed: 610.3480999469757

```

注：默认使用当前目录下的`env.json`配置文件，从中文翻译为英文；也可以通过配置参数指定，参数配置参考后面的参数说明。

## 参数说明


|参数|说明|默认值|样例|
|--|--|--|--|
|-c|api配置文件|env.json|-c local_env.json|
|-f|翻译源语言|中文|-f 日文|
|-t|翻译目标语言|英文|-t 中文|
|-i|翻译的输入源文件|空|-i input.md|
|-o|翻译后输出的文件|空|-o output.md|


