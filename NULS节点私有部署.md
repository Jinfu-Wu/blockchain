## NULS节点私有部署

### 环境准备

- 一台服务器 / 虚拟机（1核2G以上）
- Ubuntu18.04操作系统
- JDK11
- Maven
- GIT

JDK11和Maven环境配置参考：https://blog.csdn.net/qq_38270106/article/details/97764483，配置结果如下：

![image-20210908103847679](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908103847679.png)

![image-20210908103928397](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908103928397.png)

注意把上面`/root/soft/xxx`替换成你的JDK11和MAVEN解压路径。

### * 配置MAVEN镜像

进入`apache-maven-xxx/conf/setting.xml`，找到`mirrors`，添加如下配置：

```xml
    <!-- 阿里云仓库 -->
    <mirror>
        <id>alimaven</id>
        <mirrorOf>central</mirrorOf>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
    </mirror>
 
 
    <!-- 中央仓库1 -->
    <mirror>
        <id>repo1</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://repo1.maven.org/maven2/</url>
    </mirror>
 
 
    <!-- 中央仓库2 -->
    <mirror>
        <id>repo2</id>
        <mirrorOf>central</mirrorOf>
        <name>Human Readable Name for this Mirror.</name>
        <url>http://repo2.maven.org/maven2/</url>
    </mirror>
```

###  节点部署

```shell
git clone https://github.com/nuls-io/nuls-chainbox.git chainbox
```

目录如下：

![image-20210908111626978](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908111626978.png)

- 进入example目录下，执行`./package`构建加密邮件模块
- 构建结束后输出`============ PACKAGE FINISH 🍺🍺🍺🎉🎉🎉 ===============`
- 回到chainbox目录，执行`./tools -p example`进行项目部署
- 部署结束同样输出`============ PACKAGE FINISH 🍺🍺🍺🎉🎉🎉 ===============`，此时可以看到多了`NULS_WALLET`文件夹
- 进入NULS_WALLET文件夹，执行`./start-dev`命令，将启动节点
- 执行`./check-status`命令查看节点启动状态

![image-20210908112549592](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908112549592.png)

- 节点启动成功后，执行`./cmd`命令进入控制台，控制台可以[执行命令](https://docs.nuls.io/zh/Guide/g_linux_tutorial.html#%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8)对节点进行交互

![image-20210908112730397](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908112730397.png)

- 在控制台导入种子节点，注意将密码设置位`nuls123456`

![image-20210908112849207](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908112849207.png)

- 查看节点是否出块（默认出块时间位10s，10s以后可以看到高度变化，但必须导入种子节点才会出块）。高度不为0，说明节点已经开始运行

![image-20210908113011792](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908113011792.png)

- 导入两个富有的地址（密码可以自己随便设置）

```shell
import 477059f40708313626cccd26f276646e4466032cabceccbf571a7c46f954eb75
import 8212e7ba23c8b52790c45b0514490356cd819db15d364cbe08659b5888339e78
```

- 查看下余额，遇到异常不用慌张，看下报错信息，是`cross-chain`模块没有加上导致，不影响

![image-20210908113250544](C:\Users\linf.z\AppData\Roaming\Typora\typora-user-images\image-20210908113250544.png)

### 其它

节点部署完成后，可以通过控制台跑一些命令，体验下真实的区块链可以进行哪些操作、有哪些功能。如果想进一步学习，可以去看`example`的代码，尝试自己做一些修改，并替换覆盖掉原来的example，再重新执行`./package`、`./tools -p example`命令，达到模块更新的目的（记得先停掉节点，构建完再重新启动）。

官方文档：https://docs.nuls.io/zh/Docs/c_chain_box.html



