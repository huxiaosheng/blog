# linux guide for Developers

## 文件基本操作

### 复制文件

```
cp test1 test2
```



### 复制文件夹

```
cp -r test1 test2
```



### 移动

```
mv test1 test2/
```





### 重命名

````
mv test1 test2     //如果test2存在则为移动目标
````



### 创建文件

````
touch aa	
touch .aa   //加点创建隐藏文件
````



### 创建文件夹

```
mkdir test
```



### 删除文件

```
rm test
```



### 删除文件夹

```
rm -r test
```





### 浏览文件

```
less test	//内容q可以退出
```





## 简单的命令

`date`	时间

`cal`	日历

`df`		磁盘剩余空间

`free`	空闲内存的数量







## 碎片操作

### wget

从指定的URL下载文件。

```
wget http://baidu.com
```



### cat

连接文件并打印到标准输出设备上，cat经常用来显示文件的内容.



### echo 

在shell打印变量的值，或者直接输出指定的字符串 

**PS:**PHP中用`echo` 打印输出



### grep

强大的文本搜索工具，能使用正则表达式搜索文本，并把匹配的行打印出来。

```

```



### sudo

用来以其他身份来执行命令，预设的身份为root。在`/etc/sudoers`中设置可执行sudo 指令的用户。



## 常用的解压和压缩

###  unzip 

```
unzip  happygrep-master.zip  //解压zip格式的文件夹
```



### zip

```
zip -r happygrep-master.zip happygrep-master/   //压缩文件
```



### tar zxvf

```
tar zxvf wget-1.11.1.tar.gz    //解压tar.gz格式文件
```



### tar zcvf

```
tar zcvf wget-1.11.1.tar.gz  wget-1.11.1/     //压缩文件
```



### tar jxvf

```
tar jxvf weget-1.11.2.tar.bz2	//解压tar.bz2格式文件
```



### tar jcvf

```
tar jcvf weget-1.11.2.tar.bz2 weget-1.11.2/		//压缩文件
```





## 用户和文件权限

### chmod

用来更改文件或目录的权限。

- `u`	User，文件或者目录的拥有者
- `g`    Group，文件或目录的所属群组
- `o`     Other，出了文件或目录拥有者或所属群组之外


- `r`读取权限
- `w`写入权限
- `x`执行权限

```
chmod u+x a.sh
```



## 重定向

### stdin—0（标准输入）

标准输入文件，一般情况下在键盘上输入数据，那么数据会放到标准输入文件 



### stdout—1（标准输出）

标准输出文件 



### stderr—2（标准错误）

 标准错误输出文件



### " > " redirect stdout  输出重定向符

把一个程序的正常输出保存到一个文件当中

​	重定向将输入文本**通过截取模式**保存到文件：

```
echo "this is a text line one" > text.txt
```

写入到文件之前，文件内容首先会被清空



​	重定向将输入文本**通过追加模式保存到文件**

```
echo "hello world" >> text.txt
```

写入到文件之后，会追加到文件结尾



### "2>"重定向标准错误输出

```
ls shit 2> out.txt
//ls shit 为错误命令，报的错误会重定向out.txt 文件中
```





## 进程

`ps`		**查询进程**

`ps aux`		**查看详细的进程**

`kill -9 31748`	**杀死进程**

`vim &`		**后台运行进程**





## 小tips



##### ctrl+a   回到行首



## 网络操作

### ssh连接

1. 在本地执行 `ssh-keygen`，生成ssh公钥和秘钥
2. 将秘钥复制到 远程服务器 `ssh-copy-id root@106.14.166.30` ，这样下次在连接就不需要输入密码了