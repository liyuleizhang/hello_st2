# stackstorm 测试pack
在stackstorm服务中执行添加pack
```shell
st2 pack install https://github.com/liyuleizhang/hello_st2.git
```

## 文件说明
### 1.pack包图片icon.png
icon.png文件名固定,位置必须pack包根目录下
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-133504.png)

![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-133929.png)
### 2.pack包信息文件pack.yaml
pack.yaml文件名固定,位置必须pack包根目录下
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-133219.png)

ref: pack包名称，只能英文，建议与github库名称一致
```shell
ref: hello_st2
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-134114.png)

name: pack包名称，只能英文，可以当做说明使用，web页面不显示，安装的时候显示
description: pack包说明，可中文web不显示，安装的时候显示
keywords： 搜索包时使用的关键词
version： pack包版本，自定义，格式0.0.0，安装的时候显示
python_versions： stackstorm使用的python版本，2或者3，版本号不对应安装会失败
dependencies：依赖包存放目录，在根目录下的core文件夹内，如不需要依赖，本段可注释
author: 脚本作者名称，可中文，安装的时候显示
email: 脚本作者邮箱账号
contributors： 支持此pack包的其他人信息，可注释
```shell
name: Hello StackStorm
description: Simple pack containing examples of sensor, rule, and action.
keywords:
    - example
    - test
version: 3.3.0
python_versions:
  - "3"
dependencies:
  - core
author: StackStorm, Inc.
email: info@stackstorm.com
contributors:
  - "John Doe1 <john.doe1@gmail.com>"
  - "John Doe2 <john.doe2@gmail.com>"
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-135245.png)

### 3.脚本执行文件actions/greet.yaml
actions文件夹内的yaml文件为pack包中的脚本，每一个文件为一个脚本，文件名任意，非中文
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-174603.png)

name：为脚本名称
pack：所属pack，一般为pack包名称,对应pack.yaml文件的ref,可不写
```shell
name: greet
pack: hello_st2
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-175212.png)

runner_type:类型描述，不可中文
```shell
runner_type: "local-shell-script"
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-180420.png)

description: 脚本描述（可中文）
```shell
description: 脚本描述（可中文）
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-180554.png)

enabled: 未测试
```shell
enabled: true
```

entry_point：执行的shell脚本，脚本文件同本文件在同一目录
```shell
entry_point: greet.sh
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-180853.png)

脚本内容

![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-181514.png)

parameters：输入变量
```shell
parameters:  #大栏目名称
    greeting:	#输入框名称
        type: string	#未测试
        description: greeting输入框提示内容（可中文）
        required: true #出现必填提示提示*，true和false
        position: 1	#输入内容在脚本中命名为1，如上图可在greet.sh脚本中用$1带入输入内容
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-181357.png)