# spring-boot-starter-demo


## 1. 部署合约
使用控制台部署HelloWorld合约; 或者使用项目测试用例中的deploy用例部署合约。部署完成后，请记录合约地址，后续会用到。

## 2.证书拷贝
请将配置文件拷贝到生成工程的conf目录或src/main/resources/conf目录下。

## 3. 配置连接节点
请修改application.properties，该文件包含如下信息：
```
### Java sdk configuration
cryptoMaterial.certPath=conf
network.peers[0]=127.0.0.1:20200
#network.peers[1]=127.0.0.1:20201

### System configuration
system.groupId=1
system.privateKey=

### Contract configuration
contract.helloWorldAddress=

### Springboot configuration
server.port=8080
server.session.timeout=60
banner.charset=UTF-8
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss
spring.jackson.time-zone=GMT+8


```
其中：
- java sdk configuration配置部分与[javasdk](https://fisco-bcos-documentation.readthedocs.io/zh_CN/latest/docs/sdk/java_sdk/configuration.html)配置一致。
    * 其中需要用户将network.peers[0]=127.0.0.1:20200更换成实际的链节点监听地址。
- System configuration包含群组、私钥等配置。
    * system.hexPrivateKey是16进制的私钥明文，可在测试用例中的keyGeneration生成。如果为空，会随机生成一个。
- Contract confguration包含合约配置，用户需要更换成前面部署过的合约地址。


## 4. 编译和运行
您可以在idea内直接运行，也可以编译成可执行jar包后运行：

```
cd spring-boot-starter-demo
gradle bootJar
cd dist
```
会在dist目录生成spring-boot-starter-demo-exec.jar，可执行此jar包：
```
java -jar spring-boot-starter-demo-exec.jar
```
随后，可在浏览器内输入:
```
http://127.0.0.1:8080/hello/set?n=hello
```
返回示例：
```
0x1c8b283daef12b38632e8a6b8fe4d798e053feb5128d9eaf2be77c324645763b
```

```
http://127.0.0.1:8080/hello/get
```
返回示例：
```
["hello"]
```