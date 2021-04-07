# stackstorm 测试pack
在stackstorm服务中执行添加pack
```shell
st2 pack install https://github.com/liyuleizhang/hello_st2.git
```

## 文件说明
### 脚本执行文件actions/greet.yaml
actions文件夹内的yaml文件为pack中的脚本，每一个文件为一个脚本，文件名任意，非中文
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-174603.png)

name：为脚本名称
pack：所属pack，一般为pack文件夹名称
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
        required: true #此输入框必填提示*
        position: 1	#输入内容在脚本中命名为1，如上图可在greet.sh脚本中用$1带入输入内容
```
![Image text](https://raw.githubusercontent.com/liyuleizhang/img/main/hello_st2/WX20210407-181357.png)