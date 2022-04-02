[![](https://jitpack.io/v/chenjim/JitpackDemo.svg)](https://jitpack.io/#chenjim/JitpackDemo)

### 安卓上传aar到 jitpack 仓库使用和示例

> https://jitpack.io/ 仓库使用示例 <https://github.com/chenjim/JitpackDemo>  
> 本文首发地址 <https://blog.csdn.net/CSqingchen/article/details/119816973>  

1. 增加 ./jitpack.yml 使用 jdk11

2. ./build.gradle 中增加 `maven { url 'https://jitpack.io' }`

3. ./settings.gradle 中增加 `maven { url 'https://jitpack.io' }`

4. ./jplib/build.gradle 中增加 `id 'maven-publish'`   
   同时增加 afterEvaluate
   字段所有内容，参考 [build.gradle](https://github.com/chenjim/JitpackDemo/blob/main/jplib/build.gradle)

   ```Groovy
   afterEvaluate {
       publishing {
           publications {
               // Creates a Maven publication called "release".
               release(MavenPublication) {
                   from components.release
                   //建议和github地址对应，否则对jitpack无效
                   groupId = 'com.github.chenjim'
                   //建议和github仓库名称对应，否则对jitpack无效  
                   artifactId = 'JitpackDemo'
                   //建议和release的tag相同，否则对jitpack无效
                   version = '0.1.0'
               }
           }
       }
   }
   ```

5. 打开 github 仓库，如 <https://github.com/chenjim/JitpackDemo>, 点击 `Create a new release`  
   再次添加release，打开 <https://github.com/chenjim/JitpackDemo/releases>,点击 `Draft a new release`  
   `Tag version` 要和上步骤的相同

6. 用 github 账户授权登录 <https://jitpack.io/> 可以看到仓库 JitpackDemo  
   会自动编译，并记录编译日志，没有问题，就可以引用了

7. 项目使用：添加 `maven { url 'https://jitpack.io' }`  
   添加 `implementation 'com.github.chenjim:JitpackDemo:0.1.0'`
   