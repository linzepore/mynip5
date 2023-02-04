# mynip5
my nip5 certification

# Damus紫标认证

## 紫标是什么

类似于twitter的蓝色认证，其实就是给Damus加一个NIP-05 Verification，一个认证，毕竟去中心化出现的乱象其实已经可见了，Global一堆广告...

## 现成的方案

- 利用他人便捷搭建，可以看看这个博主的

​		https://www.youtube.com/watch?v=Fx7JQnTMlKw

- 利用官方直接买一个 https://snort.social/

### 缺点

优点显而易见，前者对不玩域名的兄弟来说是方便，但是在social上会出现未认证的效果；后者费钱。建议有能力的同学来尝试一下~（**装逼装到底 **）

## 自行搭建的方案

### 准备内容：DNS服务器、GitHub/服务器、域名

因为我这个域名是购自国外，所以我是通过GithubPages进行，如果是自己服务器，可以参考这个->http://tools.zepo.re/ecdb1f34，原理上也就是在服务器上存一个json文件而已，重点可能就是在hex格式转换吧，我在这踩了个坑┭┮﹏┭┮

如果选择国内域名，一些运营商可能要求备案，且服务器国内国外都可；如果选择国外域名，服务器只能选择国外的

| 域名 | 服务器 | 备案                   |
| ---- | ------ | ---------------------- |
| 国内 | 国内   | 都要备案               |
| 国外 | 国外   | 不用备案               |
| 国内 | 国外   | 不用备案（域名看情况） |
| 国外 | 国内   | 想什么呢，行不通       |
| 国外 | 香港   | 不用备案               |

## 搭建

### 过程

1) DNS服务器上增加以下的任一记录，指向GitHub Pages

```
| Type | Host           | Answer          | TTL | Priority |
|------|----------------|-----------------|-----|----------|
| A    | YOURDOMAIN.COM | 185.199.108.153 | 300 |          |
| A    | YOURDOMAIN.COM | 185.199.109.153 | 300 |          |
| A    | YOURDOMAIN.COM | 185.199.110.153 | 300 |          |
| A    | YOURDOMAIN.COM | 185.199.111.153 | 300 |          |
```

2. 创建新的 github 存储库，命名为`new`

![image-20230205051317277](C:\Users\Linzepore\AppData\Roaming\Typora\typora-user-images\image-20230205051317277.png)

![image-20230205051429500](C:\Users\Linzepore\AppData\Roaming\Typora\typora-user-images\image-20230205051429500.png)

3. 将公钥或者私钥（为隐私保障，建议还是用公钥）复制之后，到网站[damus key converter](https://damus.io/key/)转换成十六进制
4. 创建新文件 `new/.well-known/nostr.json`

4. 写入`nostr.json`的内容

```
{
  "names": {
    "bob": "e88a691e98d9987c964521dff60025f60700378a4879180dcbbb4a5027850411"
  }
}
```

其中，`blob`是前缀，`e88a691e98d9987c964521dff60025f60700378a4879180dcbbb4a5027850411`是刚刚转换的十六进制公钥

5. 在根目录处新建名为`_config.yml`的文件，写入这一行

```
include: [".well-known"]
```

6. 在仓库名页面地址末端加上`/settings/pages`，也就是`github.com/[用户名]/[仓库名]/settings/pages`；或者直接点击该仓库的设置进入Pages设置

![image-20230205053712552](C:\Users\Linzepore\AppData\Roaming\Typora\typora-user-images\image-20230205053712552.png)

7. 在"Build and deployment"下面选择 "Deploy from branch" ，然后选择 "Main/Master" 分支
8. “Custom domain”这里填入域名并“Save”，同时勾上“Enforce HTTPS ”

![image-20230205054136487](C:\Users\Linzepore\AppData\Roaming\Typora\typora-user-images\image-20230205054136487.png)

### 测试及应用

#### 测试

按照`<域名>/.well-known/nostr.json?name=前缀`的形式进入，出现完整json就说明基本ok了

#### 应用

* 可以在Damus-NIP-05处直接进行填写，格式就是`前缀@域名`
* 也可以在[Fiatjaf/NOS2X：Nostr 签名器扩展 (github.com)](https://github.com/fiatjaf/nos2x)
* 或者是[Astral](astral.ninja/settings)

这三个应该都属于Nostr的，资料更新会同步，但是有点小bug，资料更新形式是采用覆盖式的

### nostr（Damus）的各种key

关于key的规定，是在第19个文档（[nips/19.md at master · nostr-protocol/nips (github.com)](https://github.com/nostr-protocol/nips/blob/master/19.md)）里面，设计安全性蛮高的，具体内容有兴趣进链接细看，我这里截出他的例子，可以看出，公钥、私钥最终转换成相同的十六进制的key，公钥私钥则在UI界面的操作

![image-20230205054641985](C:\Users\Linzepore\AppData\Roaming\Typora\typora-user-images\image-20230205054641985.png)

参考官方文档：

[NIP5（GitHub.com）](https://github.com/nostr-protocol/nips/blob/master/05.md)

[NVK.org / How to setup NIP5 verification using Github Pages](https://nvk.org/n00b-nip5)

[NIPS/19.MD at Master NIPS (github.com)](https://github.com/nostr-protocol/nips/blob/master/19.md)

[How To Get Your Nostr Account NIP-05 Verified - The Bitcoin Manual](https://thebitcoinmanual.com/articles/nostr-account-nip-05-verified/)
