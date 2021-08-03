# IDEA入门设置使用


# IDEA入门设置及使用

## 下载安装



{{< admonition  "下载地址">}}

`https://www.jetbrains.com/idea/`

{{< /admonition >}}

一路下一步即可，注意选择`Evaluate for free`试用。

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728161225.png " ")

## 配置JAVA和MAVEN

- 打开`setting`设置&rarr;选择`Build,Execution,Deployment`&rarr;`BuildTools`&rarr;`Maven`
- 同时设置新建项目的默认设置，`File`&rarr;`New projects Setting`&rarr;`Setting For New Projects` 同上设置

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728162334.png " ")

- 新建项目，选择`File` &rarr; `Project Structure`配置或下载新的jdk

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728164152.png " ")



## 常用配置及代码模板

### 调高JVM内存

找到`IDEA`默认安装目录&rarr;`bin`目录，打开以`vmoptions`为后缀的文件，修改参数：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210729144801.png " ")



| 参数                        | 说明                                                 |
| :-------------------------- | ---------------------------------------------------- |
| `-Xms`                      | 初始化堆内存大小                                     |
| `-Xmx`                      | 堆内存最大值                                         |
| `-XX:ReservedCodeCacheSize` | 代码缓存，用于存储已编译方法生成的本地代码（字节码） |

值的大小根据自己电脑的内存以及自己需要修改，修改值之后，如果idea不卡顿而内存占用率又不过90即可

```
-Xms1024m
-Xmx2048m
-XX:ReservedCodeCacheSize=1024m
```



### 自定义模板

- `main`方法：`psvm`

- 控制台输出：`sout`
- `int`常量：`psfi`
- `String`常量：`psfs`

以上模板可在实时模板参考，自定义方法注释模板操作如下:

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728165303.png " ")



```
*
 * $END$
 *
 * @param $methodParameters$
 * @return $methodReturnType$
 * @since $date$ $time$
 */
```

模板代码可自定义，设置完成点击`Change`选中`Java`

### 文件和代码模板

在新建该文件的时候会使用配置好的模板，根据需求选择类，接口，枚举，注解等

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728170616.png " ")

模板代码：

```
/**
* $DESCRIPTION
*
* @author Crush-Cmj
* @since $DATE $TIME
*/
```



### 面包屑导航配置

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728170231.png " ")

配置效果如图：

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728170329.png " ")



## 常用快捷键

- 万能键： `Alt + ENTER`

- 选择项目视图：`ALT + F1`

- **切换标签页**： `ALT + LEFT/RIGHT`

- 跳转方法：`ALT ` +  &uarr;  &darr;

- 新增文件： `ALT + F`&rarr;`N`&rarr;选择想要新增的文件

- **运行当前文件**： `CTRL + SHIFT + F10`

- 运行上次文件： `SHIFT + F10`

- **重命名**： `SHIFT + F6`

- 定位错误： `SHIFT+F2`

- 以`DEBUG`模式运行上次运行的文件：`SHIFT `+ F9

- 选择运行文件： `Alt + SHIFT + F10 `

- **选择文件以`DEBUG`模式运行**：`ALT + SHIFT + F9`

- 搜索全部： 双击`SHIFT`

- 运行全部： 双击`CTRL`

- 逐词跳跃：`CTRL + LEFT/RIGHT`

- 删除到词尾：`CTRL+DELETE`

- 关闭标签页： `CTRL+F4`

- 查看结构：`CTRL+F12`

- **跳转到引用位置**：`CTRL + B` / `CTRL + ALT + F7`

- 跳转到接口实现位置：`ALT + B` 

- 搜索： `CTRL+F`

- 替换： `CTRL+R`

- 重做（撤销的撤销）：`CTRL + SHIFT + Z`  个人改成了(`CTRL + Y`)

- **重构（提取方法）**：`CTRL + ALT + M`  个人改成了（`ALT + M`）

- 在文件中查找： `CTRL + SHIFT + F`

- 在文件中搜索并替换： `CTRL + SHIFT + R`

- 打开项目结构：`CTRL + ALT + SHIFT + S` 个人改成了（`CTRL + SHIFT + S`）

- 新建草稿文件（json）：`CTRL + SHIFT + ALT + INSERT`

- **代码补全**： `CTRL+SHIFT+ENTER`

- 方法移位：`CTRL + SHIFT + ` &uarr;  &darr;

- 单行代码移位：`ALT + SHIFT + ` &uarr;  &darr;

- 格式化代码： `CTRL + ALT + L`

- 删除无用导包：  `CTRL + ALT + O`

- 选择代码行/块：`CTRL + W`    撤回：`CTRL + SHIFT + W`

- **环绕方式**（`if，catch`）：`CTRL + ALT + T`个人改成了（`ALT + T`）

  



## 常用开发插件

- `CodeGlance`：代码树
- `Gitee`  ：同步代码插件
- `Translation` ：翻译插件
- `lombok`  ：链式加载插件（重写`set`）
- `IDE Eval Reset` ：重置试用期插件
- `Git Tool box` ：多人同步代码日志插件
- `RoboPOJOGenerator` ：JSON串转对象插件
- `MybatisLogFormat`：格式化`sql`日志为`sql`语句

- `Chinese (Simplified) Language Pack` ：汉化包

- `Alibaba Java Coding Guidelines` ：阿里代码规范插件

- `CamelCase` ：便利命名插件，快捷键`Alt+Shift+U`切换驼峰命名，中划线，下划线等等

- `Codota AI Autocomplete for Java and JavaScript`：联想开源社区代码用法，快捷键`ctrl+shift+O`

  

  

### `IDE Eval Reset` 使用

一般来说，在 IDE 窗口切出去或切回来时（窗口失去/得到焦点）会触发事件，检测是否长时间（`25`天）没有重置，给通知让你选择。也可以手动唤出插件的主界面，如果 IDE 没有打开项目，点击`齿轮` -> `Eval Reset`

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210201160312752.png " ")

如果 IDE 打开了项目，点击菜单：`Help` -> `Eval Reset`

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210729115600.png " ")

唤出的插件主界面中包含了一些显示信息，`2`个按钮，`1`个勾选项

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210729115650.png " ")

- 按钮：`Reload` 用来刷新界面上的显示信息。
- 按钮：`Reset` 点击会询问是否重置试用信息并**重启 IDE**。选择`Yes`则执行重置操作并**重启 IDE 生效**，选择`No`则什么也不做。（此为手动重置方式）
- 勾选项：`Auto reset before per restart` 如果勾选了，则自勾选后**每次重启/退出 IDE 时会自动重置试用信息**，你无需做额外的事情。（此为自动重置方式）





### `RoboPOJOGenerator`使用

复制`JSON`串，在需要转换为`JAVA`类的文件右键新建，选择生成来源于`JSON`串的实体类，选择序列化框架

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/20210728173157.png " ")

![](https://gitee.com/cao-lianjie/pic-go/raw/master/img/image-20210729111314248.png " ")

### `lombok`使用

- （[官方文档](https://projectlombok.org/features/all)）安装插件，新建工程时导入`POM`依赖`JAR`包

```xml
 <!--lombok插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
```

- **`@Data`**

@Data最常用的注解之一。注解在类上，提供该类所有属性的getter/setter方法，还提供了equals、canEqual、hashCode、toString方法。

- **@Accessors**

@Accessors用于配置getter和setter方法的生成结果，一般与`@Data`配合使用；有三个属性：

`fluent`的中文含义是流畅的，设置为`true`，则`getter`和`setter`方法的方法名都是基础属性名，且setter方法返回当前对象。如下：

```java
@Data
@Accessors(fluent = true)
public class User {
    private Long id;
    private String name;
    
    // 生成的getter和setter方法如下，方法体略
    public Long id() {}
    public User id(Long id) {}
    public String name() {}
    public User name(String name) {}
}
```

`chain`的中文含义是链式的，设置为`true`（默认），则`setter`方法返回当前对象。如下

```java
@Data
@Accessors(chain = true)
public class User {
    private Long id;
    private String name;
    
    // 生成的setter方法如下，方法体略
    public User setId(Long id) {}
    public User setName(String name) {}
}
```

`prefix`的中文含义是前缀，用于生成`getter`和`setter`方法的字段名会忽视指定前缀（遵守驼峰命名）如下

```java
@Data
@Accessors(prefix = "p")
class User {
	private Long pId;
	private String pName;
	
	// 生成的getter和setter方法如下，方法体略
	public Long getId() {}
	public void setId(Long id) {}
	public String getName() {}
	public void setName(String name) {}
}
```

- **@AllArgsConstructor**

@AllArgsConstructor作用于类上，为该类提供一个包含全部参的构造方法，注意此时默认构造方法不会提供。

- **@NoArgsConstructor**

@NoArgsConstructor作用于类上，提供一个无参的构造方法。可以和@AllArgsConstructor同时使用，此时会生成两个构造方法：无参构造方法和全参构造方法。

- **@NonNull**

作用于属性上，提供关于此参数的非空检查，如果参数为空，则抛出空指针异常。

```java
public class Demo {
	@NonNull
	private int id;
	private String remark;
}
```

- **@RequiredArgsConstructor**

作用于类上，由类中所有带有@NonNull注解或者带有final修饰的成员变量作为参数生成构造方法。

- **@Cleanup**

作用于变量，保证该变量代表的资源会被自动关闭，默认调用资源的close()方法，如果该资源有其它关闭方法，可使用@Cleanup(“methodName”)来指定。

```java
public void jedisExample(String[] args) {
    try {
        @Cleanup Jedis jedis =   redisService.getJedis();
    } catch (Exception ex) {
        logger.error(“Jedis异常:”,ex)
    }
}
```

效果相当于：

```java
public void jedisExample(String[] args) {

    Jedis jedis= null;
    try {
        jedis = redisService.getJedis();
    } catch (Exception e) {
        logger.error(“Jedis异常:”,ex)
    } finally {
        if (jedis != null) {
            try {
                jedis.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```












