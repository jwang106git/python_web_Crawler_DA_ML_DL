# 1 MySQL基础

## 1.1 MySQL 简介

MySQL是一个关系型数据库管理系统，由瑞典MySQL AB公司开发，后来被Sun公司收购，Sun公司后来又被Oracle公司收购，目前属于Oracle旗下产品。

* 使用C和C++编写，并使用了多种编译器进行测试，保证源代码的可移植性

* 支持多种操作系统，如Linux、Windows、AIX、FreeBSD、HP-UX、MacOS、NovellNetware、OpenBSD、OS/2 Wrap、Solaris等

* 为多种编程语言提供了API，如C、C++、Python、Java、Perl、PHP、Eiffel、Ruby等

* 支持多线程，充分利用CPU资源

* 优化的SQL查询算法，有效地提高查询速度

* 提供多语言支持，常见的编码如GB2312、BIG5、UTF8

* 提供TCP/IP、ODBC和JDBC等多种数据库连接途径

* 提供用于管理、检查、优化数据库操作的管理工具

* 大型的数据库。可以处理拥有上千万条记录的大型数据库

* 支持多种存储引擎

* MySQL 软件采用了双授权政策，它分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，尤其是开放源码这一特点，一般中小型网站的开发都选择MySQL作为网站数据库

* MySQL使用标准的SQL数据语言形式

* Mysql是可以定制的，采用了GPL协议，你可以修改源码来开发自己的Mysql系统

* 在线DDL更改功能

* 复制全局事务标识

* 复制无崩溃从机

* 复制多线程从机

**MySQL默认配置和我们学习时中：host：localhost；port：3306**

**在学习过程中，英文好的朋友可以直接学习官方文档，讲的更通俗易懂。本书仅仅是将mysql基本操作介绍给python人员，并非深入研究学习mysql。**

![](/assets/mysql_document.png)

## 1.2 MySQL 终端启动、图形化操作工具Navicat

### Linux系统的数据库启动命令

**启动命令**

```
sudo service mysql start
```

**停止命令**

```
sudo service mysql stop
```

**重启命令**

```
sudo service mysql restart
```

### 终端连接启动

#### 1、连接命令

| 命令格式 | mysql -h host -u user -p password |  |
| :--- | :--- | :--- |


##### mac：

以下命令运行后输入密码即可。

```
PATH=“$PATH”:/usr/local/mysql/bin
mysql -u root -p
```

##### ![](/assets/mac.png)

##### linux：

```
shell> mysql -h host -u user -p
```

![](/assets/linux_mysql.png)

#### 2、结束连接的命令：

| 命令 | QUIT  或 EXIT 或ctrl+d |
| :--- | :--- |


### 图形化操作工具Navicat

为了更好的理解后续学习时用SQL操作后的数据库数据影响，我们在此推荐除了mysql官方的workbench以外的图形化操作工具Navicat。图形化的操作在学习之初能更好的帮我们理解数据库的结构和逻辑。

Navicat是一套快速、可靠并价格相当便宜的数据库管理工具，专为简化数据库的管理及降低系统管理成本而设。它的设计符合数据库管理员、开发人员及中小企业的需要。Navicat是以直觉化的图形用户界面而建的，让你可以以安全并且简单的方式创建、组织、访问并共用信息。Navicat适用于三种平台 - Microsoft Windows、Mac OS X 及Linux。它可以让用户连接到任何本机或远程服务器、提供一些实用的数据库工具如数据模型、数据传输、数据同步、结构同步、导入、导出、备份、还原、报表创建工具及计划以协助管理数据。如下图为其截面图和说明。具体操作可以查看网页：[https://www.cnblogs.com/smyhvae/p/4030506.html](https://www.cnblogs.com/smyhvae/p/4030506.html)

![](/assets/Navicat_page.png)

连接数据库操作：点击左上方的connection并选择MySQL，然后在弹出的New connection-SQL窗口填写服务器地址、账号信息和编码信息后即可连接到数据库服务器。

![](/assets/navicate_connection.png)

## 1.3 MySQL 基础SQL操作语句

### SQL\(Structured Query Language\)

SQL是结构化查询语言，是一种用来操作RDBMS的数据库语言，当前关系型数据库都支持使用SQL语言进行操作,也就是说可以通过 SQL 操作 oracle,sql server,mysql,sqlite 等等所有的关系型的数据库

* SQL语句主要分为：
  * **DQL：数据查询语言，用于对数据进行查询，如select**
  * **DML：数据操作语言，对数据进行增加、修改、删除，如insert、udpate、delete**
  * TPL：事务处理语言，对事务进行处理，包括begin transaction、commit、rollback
  * DCL：数据控制语言，进行授权与权限回收，如grant、revoke
  * DDL：数据定义语言，进行数据库、表的管理等，如create、drop
  * CCL：指针控制语言，通过控制指针完成表的操作，如declare cursor
* 对于web程序员来讲，
  重点是数据的crud（增删改查），必须熟练编写DQL、DML，能够编写DDL完成数据库、表的操作
  ，其它语言如TPL、DCL、CCL了解即可
* SQL 是一门特殊的语言,专门用来操作关系数据库
* **不区分大小写**

### MySQL脚本的基本组成

与常规的脚本语言类似, MySQL 也具有一套对字符、单词以及特殊符号的使用规定, MySQL 通过执行 SQL 脚本来完成对数据库的操作, 该脚本由一条或多条MySQL语句\(SQL语句 + 扩展语句\)组成, 保存时脚本文件后缀名一般为 .sql。在控制台下, MySQL 客户端也可以对语句进行单句的执行而不用保存为.sql文件。

**标识符：**标识符用来命名一些对象, 如数据库、表、列、变量等, 以便在脚本中的其他地方引用。MySQL标识符命名规则稍微有点繁琐, 这里我们使用万能命名规则: 标识符由字母、数字或下划线\(\_\)组成, 且第一个字符必须是字母或下划线。  
对于标识符是否区分大小写取决于当前的操作系统, Windows下是不敏感的, 但对于大多数 linux\unix 系统来说, 这些标识符大小写是敏感的。\(SQ关键字不区分大小写\)

**关键字: **MySQL的关键字众多, 这里不一一列出, 在学习中学习。 这些关键字有自己特定的含义, 尽量避免作为标识符。

**语句: **MySQL语句是组成MySQL脚本的基本单位, 每条语句能完成特定的操作, 他是由 SQL 标准语句 + MySQL 扩展语句组成。

**函数:** MySQL函数用来实现数据库操作的一些高级功能, 这些函数大致分为以下几类: 字符串函数、数学函数、日期时间函数、搜索函数、加密函数、信息函数。

### MySQL 基础数据类型与约束

作为数据库，应当具备**数据完整性**，这是硬性要求。那如何实现呢？我们来看看数据库的组成：一个数据库就是一个完整的业务单元，可以包含多张表，数据被存储在表；在表中为了更加准确的存储数据，保证数据的正确有效，可以在创建表的时候，为表添加一些强制性的验证，包括**数据字段的类型、约束。**接下来我们来列举介绍MySQL常见的数据类型和约束。

数据库是用来存储数据的，而实际应用中希望数据占用磁盘空间越小越好。所以，**在数据库中使用数据类型的原则就是：够用就行，尽量使用取值范围小的，而不用大的，这样可以更多的节省存储空间**。因此，相比一般的编程语言数据类型，MySQL的三大数据类型\(数值、时间、字符类\)划分了很多占内存更小的子数据类型。

##### 数值类型

| 类型 | 字节大小 | 有符号范围\(Signed\) | 无符号范围\(Unsigned\) |
| :--- | :--- | :--- | :--- |
| TINYINT | 1 | -128~127 | 0~255 |
| SMALLINT | 2 | -32768~32767 | 0~65535 |
| MEDIUMINT | 3 | -8388608~8388607 | 0~16777215 |
| INT/INTEGER | 4 | -2147483648~2147483647 | 0~4294967295 |
| BIFINT | 8 | $$-2^{63}$$~$$2^{63}$$ | $$2^{64}$$ |

##### 字符串

| 类型 | 字节大小 | 示例 |
| :--- | :--- | :--- |
| CHAR | 0-255 | 类型:char\(3\) 输入 'ab', 实际存储为'ab ', 输入'abcd' 实际存储为 'abc' |
| VARCHAR | 0-255 | 类型:varchar\(3\) 输 'ab',实际存储为'ab', 输入'abcd',实际存储为'abc' |
| TEXT | 0-65535 | 大文本 |

注：  
1、未列出tinytext、mediumtext、longtext  
2、二进制\(可用来存储图片、音乐等\): tinyblob、blob、mediumblob、longblob

##### 时间类型

| 类型 | 字节大小 | 示例 |
| :--- | :--- | :--- |
| DATE | 4 | '2020-01-01' |
| TIME | 3 | '12:29:59' |
| DATETIME | 8 | '2020-01-01 12:29:59' |
| YEAR | 1 | '2017' |
| TIMESTAMP | 4 | '1970-01-01 00:00:01' UTC ~ '2038-01-01 00:00:01' UTC |

枚举类

| 类型 | 示例 |
| :--- | :--- |
| enum | enum\('男'，‘女’\) |

特别说明的类型如下：

* decimal表示浮点数，如decimal\(5,2\)表示共存5位数，小数占2位
* char表示固定长度的字符串，如char\(3\)，如果填充'ab'时会补一个空格为`'ab '`
* varchar表示可变长度的字符串，如varchar\(3\)，填充'ab'时就会存储'ab'
* 字符串text表示存储大文本，当字符大于4000时推荐使用
* 对于图片、音频、视频等文件，不存储在数据库中，而是上传到某个服务器上，然后在表中存储这个文件的保存路径

#### 约束 {#约束}

* **主键primary key：物理上存储的顺序**
* 非空not null：此字段不允许填写空值
* 惟一unique：此字段的值不允许重复
* 默认default：当不填写此值时会使用默认值，如果填写时以填写为准
* 外键foreign key：对关系字段进行约束，当为关系字段填写值时，会到关联的表中查询此值是否存在，如果存在则填写成功，如果不存在则填写失败并抛出异常
* 说明：虽然外键约束可以保证数据的有效性，但是在进行数据的crud（增加、修改、删除、查询）时，都会降低数据库的性能，所以不推荐使用，那么数据的有效性怎么保证呢？答：可以在逻辑层进行控制



