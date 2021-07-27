# 基于STS的Ares5.0工程开发


#  基于STS的Ares5.0工程开发

## Ares5.0开发环境搭建

### 1.Node环境准备

#### 安装NVM

使用NVM安装Node，可以方便的切换Node版本，安装NVM之前一定要卸载已安装的 NodeJS，否则会发生冲突。

**NVM全名node.js version management，是一个node的版本管理工具**

- 下载[NVM](https://github.com/coreybutler/nvm-windows/releases)，推荐使用安装包下载，如下图

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721194523.png " ")



- 安装完成后命令行执行命令：nvm 成功出现以下代码

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721194816.png " ")

```
nvm off                     //禁用node.js版本管理(不卸载任何东西)
nvm on                      //启用node.js版本管理
nvm install <version>       //安装node.js的命名 version是版本号 例如：nvm install 8.12.0
nvm uninstall <version>     //卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
nvm list                    //显示所有安装的node.js版本
nvm list available          //显示可以安装的所有node.js的版本
nvm use <version>           //切换到使用指定的nodejs版本
```

#### 配置淘宝镜像

由于nvm默认的下载地址http://nodejs.org/dist/是外国外服务器，速度非常慢，可以切换到淘宝镜像，加快下载速度

打开nvm的安装路径：D:\software\java_softwear\nvm（我的地址），打开settings.txt，添加如下配置

```properties
root: D:\software\java_softwear\nvm
path: D:\software\java_softwear\Node.js
arch: 64 
proxy: none
node_mirror: http://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

####  安装Node

Ares中使用的版本是v12.10.0，安装命令如下：

```
nvm  install version

nvm  install v12.10.0
```

Installation complete 代表nodejs安装完成

#### 切换nodejs版本

查询所有的nodejs版本：nvm list ，切换到要使用的版本（nvm use 12.10.0）

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721200022.png " ")

#### 配置环境变量

为了全局使用nvm命令，就需要配置下环境变量,这里以win10为例:

- 环境变量：点击我的电脑···属性···高级系统设置···环境变量

- 删除系统变量：
  a. 找到系统变量删除系统自带的nvm变量：`NVM_HOME和NVM_SYMLINK`

    b. 打开path：删除nvm自动添加的变量：`Path = %NVM_HOME%;%NVM_SYMLINK%`

- 配置用户变量：

![image-20210721201317732](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210721201317732.png " ")

#### 测试node，npm是否安装成功

依次执行node，npm命令，出现以下画面则安装成功

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721201602.png  " ")

### 2.全局安装进程

确认npm，node安装成功以后，执行如下命令：

```
node install pm2 -g
```

### 3.全局安装gulp

执行如下命令安装自动化构建工具gulp：

```
npm install gulp-cli -g
```

### 4.安装插件

安装STS工具（sts-4.7.1.RELEASE），可在公司内网或[Spring官网](http://spring.io/tools/ggts/all
)下载；

将 YTStudio*.jar 复制到 sts/plugins 目录中。安装完毕后，打开 STS（或重启STS），即可使用。（新版本插件至少在YTStudio4以上）

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721202353.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722093441.png " ")

### 5.公共环境模板配置

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722084024.png " ")

- 下载 ares*.zip将 ares.zip 解压到本地的 系统⽤户根⽬录即当前默认用户（C:\Users\曹盟杰\ares）下 ，ares目录如下图所示：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721202655.png " ")

- 切换到ares目录下，打开cmd，执行命令：**npm install**，执行成功以后，生成如下文件

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721202904.png " ")

### 6.Maven配置

- 修改Maven本地库地址setting文件中localRepository标签：

```
D:\software\java_softwear\apache-maven-3.5.0\apache-maven-3.5.0\conf

<localRepository>D:/YtJavaDev</localRepository>
```

- 打开STS，选择Window -> Preferences -> Maven,设置如下：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722091557.png " ")

### 7.STS优化配置

- 编码配置（window-prefrences-General-workspace），工程编码设置为UTF-8

- 编译时校验功能关闭，提高STS速度：window-prefrences-vaildation-build一列全部去掉

- 安装properties插件，将配置文件ASCII码转换成中文

  ```
  1.下载离线安装文件：http://sourceforge.jp/projects/propedit/downloads/40156/jp.gr.java_conf.ussiy.app.propedit_5.3.3.zip/
  
  2.安装与检验:
  将得到的文件直接解压，可得到这样一个文件夹 jp.gr.java_conf.ussiy.app.propedit_5.3.3 ，直接将该文件夹复制到 STS插件目录下。
  3.重启Eclipse。
  
  4.选中 *.properties 文件，右键 - Open With ，你会看到多了一个 PropertiesEditor 子菜单。
  
  5.将PropertiesEditor设为默认的打开方式
  工具栏->Window->Preferences->General->Editors->File Associations,添加一个*.properties。
  下方的 Associated editors 栏里有 PropertiesEditor 项，选中，点击 Default 按钮。
  双击properties文件默认就会用PropEditor打开。
  ```



- SVN目录忽略设置

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722100844.png " ")

### 8.导入工程

- 本地导入：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722093618.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722093654.png " ")

- SVN导入需连接公司内网：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722094029.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722094101.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722095005.png " ")



## Ares5.0应用架构说明

Ares5.0标准版采用微服务模式开发，前端通过微服务网关（gateway）访问后台微服务。

微服务网关（gateway）和微服务之间采用dubbo进行通信（可支持http）

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721140330.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722114724.png " ")

## 工程说明

### 基本结构

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722104555.png " ")



- ares-mmc-platform：后管服务

### 工程jar包依赖

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721143005.png " ")

### 网关（ares-mobile-gateway）执行时序

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210721170205.png " ")



### cust渠道整合工程 

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722114515.png " ")

- dubbo.properties

``` properties
#dubbo服务注册中心
#测试环境
dubbo.registry.address=zookeeper://192.168.0.171:2181
#本机环境
dubbo.registry.address=zookeeper://127.0.0.1:2181
```

```properties
#dubbo注册中心组名称要与网关（getway）注册中心组配置名称一致
#dubbo.registry.group=ares.inte
dubbo.registry.group=dubbo
```



- jdbc.properties

```properties
#公司测试环境
jdbc.url=jdbc:mysql://192.168.0.141:3306/inte?useUnicode=true&characterEncoding=utf8&autoReconnect=true&failOverReadOnly=false
```

### IBusinessContext

#### 数据总线作用

- 总线在接受交易请求时创建；各组件通过数据总线进行数据存取交互；请求结束，数据总线销毁；
- 数据以`Map<String,Object>`或`List<Map<String,Object>>`等对象方式保存在总线中；
- 顶层结构为Map，包含头区、请求区、会话区、缓存区等数据区块；
- 会话区数据不能通过交易请求字段生成；调用通讯时请求中包含`SESS_`的数据为非法数据。

数据结构示意如下:

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722161713.png " ")

#### 1.头区

KEY以 `H_` 开头，如 `H_SEQ`

- API

```java
public Map getHeadMap();
public String getHeadMap(String name);
public void setHead(String name,String value);
```



- 示例

```java
String seq = ctx.getHead("H_SEQ");
或者表达式${H_SEQ}
```

#### 2.请求区

- API

```java
public <T> T getParam(String xpath);
public <T> T getParam(String xpath,Object def);
public boolean setParam(String name, Object data);
public Map getParamMap();
```

- 示例

```java
String acctNo = ctx.getParam("ACCT_NO");
int num = ctx.getParam("NUM",0);
boolean flag = ctx.getParam("FLAG",false);
//或者表达式${ACCT_NO}
```

#### 3.会话区

数据在会话期间有效；KEY以`SESS_`开头，如：`SESS_USER_NO`; 只能在组件或者代码中创建

- API

```java
//获取会话
public <T> T getSessionObject(String name);
//保存会话
public void saveSessionObject(String name, Object obj);
```

- 示例

```java
String userId = ctx.getSessionObject("SESS_USER_NO");
//或者表达式${SESS_USER_NO}
```

#### 4.缓存区

数据在临时缓存中，如：一次性会话生成，默认有效时长为120s；

- API

```java
public <T> T getSessCache(String key);
public void setCacheService(ICacheService cacheService);
```

- 示例

```java
String imgCode = ctx.getSessCache("CACHE_IMAGE_CODE");
//或者表达式${CACHE_IMAGE_CODE}
```











## 组件说明





## 后台接口服务开发流程

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210713142819.png " ")



###  1.新增接入服务

新增接入服务实际上就是利用封装工具自动生成Java类和规范输入输出字段

启动cust应用服务，切换到接入服务选项卡，点击新增接入服务

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722133259.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722134658.png " ")

每项服务都是一个接口，接口开发完成在Ares交易测试平台模拟请求数据，进行单元测试

### 2.定义报文

新增接入服务完成后，选择报文路径，定义输入输出字段，注意若接收List表单type必须取值为E

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722134841.png " ")



![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722154309.png " ")

```xml
<?xml version="1.0" encoding="utf-8"?>
<trans name="in/easy/sample10" desc="交易示例-10-查询系统时间">
	<snd>
		<field name="NUM" desc="数字" required="true"/> required="true"表示测试必输项
	</snd>
	<rcv>
		<field name="SYS_DATE" desc="服务器日期" /> 保证数据能存入总线，报文属性名称要与Java类中放入总线的Key保持一致
		<field name="FZINFO" desc="分支提示信息" />
	</rcv>
</trans>
```

### 3.设计流程及业务逻辑

点击访问路径url，创建流程文件，每个组件都是流程图上的一个节点，线条可定义进入节点的条件，当一个功能业务逻辑比较复杂时，可以将一个服务（接口）拆分成多个任务节点实现，便于查看和维护。

拖拽组件设计完流程后，点击节点设置Java类名称，设置完成保存节点信息。根据beanId创建Java类

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722140946.png " ")



![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210713163742.png " ")



![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210722140020.png " ")



参数`IBusinessContext`为数据总线,包含请求数据和将要返回的数据

```java
@Service
public class GetSysDateOp implements IAresSerivce {

	private Logger logger = LoggerFactory.getLogger(getClass());

	@Override
	public int execute(IBusinessContext ctx) {
		// TODO Auto-generated method stub
		logger.debug("-简单任务-run--");
		String date = DateUtil.todayStr();//获取当前系统时间
		ctx.setParam("SYS_DATE", date);//将获取的时间放入数据总线中，KEY值要与报文定义的KEY值保持一致
		return NEXT;
	}

}
```

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210713164557.png "")



业务代码完成，如节点涉及到数据库操作，在接入服务窗口点击对应SQL链接，自动生成xml文件，编写sql语句，定位标识写到节点设置的数据转译区`*sqlId`即`namespace.id`

点击需同步接入信息服务



### 4. 交易服务测试

服务调试工具中找到对应服务，填入服务必填项测试是否返回所需数据
















