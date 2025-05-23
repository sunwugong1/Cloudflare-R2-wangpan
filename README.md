# 利用Cloudflare R2 + Workers搭建在线网盘


[汉化修改自/longern/FlareDrive](https://github.com/longern/FlareDrive)

增加了权限系统，支持多管理员，分别授权目录

cloudflare R2是一个文件储存系统，配合Cloudflare Workers可以实现这样一个网盘系统

[文件库 (oss.ljxnet.cn)](https://oss.ljxnet.cn/)


### 搭建教程


1. fork该仓库
2. 前往Cloudflare R2新建一个R2储存桶，名称随意，创建好储存桶点击设置-启用公共开发 URL，输入allow,点击允许公开访问，复制**公共存储桶 URL**
3. 前往Cloudflare Pages新建一个站点，选择连接到Git

4.选择刚刚fork的仓库，点击开始设置

5.项目名称可以修改，其他项目保持默认不动

6.添加环境变量

| 变量名称| 值|
| --- | --- |
| PUBURL | 复制的**公共存储桶URL** |
| GUEST | public/ |
| admin:123456 | * |
| user1:123456 | user1/,userPublic/ |

以此类推，GUEST代表游客的允许写入目录

管理员则以`账号:密码`的形式设置，值代表其允许写入的目录，用`,`隔开，**请勿在前后加逗号，否则会授予所有目录的写入权限**

变量说明:

变量名称       值

GUEST         public/  # 想在别的浏览器中访问，这个变量必须添加

admin:123456  *  # 可以把admin:123456替换成自己的用户名和密码，如: rg520:Huagongzi1@

user1:123456  user1/,userPublic/  # 这个变量可以忽略，不用添加

设置好后点击**开始部署**

7.前往Pages->cloudflare-r2-wangpan->设置->函数->R2 存储桶绑定,绑定R2存储桶,变量名称必须为`BUCKET`

8.在部署页面重新部署即可
