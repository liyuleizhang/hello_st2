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

### 4.编写第一个pack
根据上面学习的内容，通过icon.png、pack.yaml、actions/echo.yaml、actions/echo.sh四个文件创建自己的第一个pack包

pack.yaml
```shell
---
ref: st2test
name: st2 test 
description: 测试StackStorm的pack包                                      
keywords:
    - example
    - test
version: 0.0.1
python_versions:
  - "3"
author: 张三
email: zhangsan@163.com.com
```
actions/echo.yaml
```shell
---
name: echo
runner_type: "local-shell-script"
description: 输出填入的echo内容
enabled: true
entry_point: echo.sh
parameters:
    echo:
        type: string
        description: 请输入任意内容，运行后将输出此内容
        required: true
        position: 1
```

actions/echo.sh
```shell
#!/bin/bash
echo "输入了:$1!"
```

在github中创建名称为pack.yaml文件下ref名称st2test的库，将icon.png、pack.yaml、actions/echo_file.yaml、actions/echo_file.sh四个文件上传到github的st2test库中

通过如下命令在StackStorm中安装st2test的pack包
```shell
docker-compose exec st2client st2 pack install https://github.com/liyuleizhang/st2test.git
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-151117.png)

在web页面依次单击ACTIONS---找到ST2TEST---单击echo---在echo输入框中输入随意内容---单击RUN运行
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/1617868758979.jpg)

在web页面依次单击HISTORY---找到st2test.echo---查看ACTION OUTPUT
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210408-160108.png)
