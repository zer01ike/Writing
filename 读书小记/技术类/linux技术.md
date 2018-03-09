# 此文为一般Linux使用的基本知识

## 使用命令帮助
### 简要查看
```sh
whatis command    #显示命令的简要说明
whatis -w "loca*" #添加正则表达式来过滤
inof command      # 更加详细的说明文档
```
### man的使用
```sh
man command #查看一个command的说明，可以用pagedown 和pageup来翻页
```
man的帮助页面分为9个类别

1. 用户可以操作的命令或者是可执行文件 
2. 系统核心可调用的函数与工具等
3. 一些常用的函数与数据库
4. 设备文件的说明
5. 设置文件或者某些文件的格式
6. 游戏
7. 惯例与协议等。例如Linux标准文件系统、网络协议、ASCⅡ，码等说明内容
8. 系统管理员可用的管理条令
9. 与内核有关的文件

```sh
man -k keyword #在某个分类中查看命令
```
### 查看路径
```sh
which command #查看程序binary文件所在的位置
whereis command #查看程序的搜索路径 
```

## 文件和目录管理
### 基本操作
文件管理主要包括文件或者目录的创建、删除、查询、移动、复制对应的是mkdir,rm,find,mv,cp

```sh
mkdir /home/test/ #创建名为test的目录
rm readme.md      #删除当前目录下的readme.md
rm -rf /home/test/#删除非空test文件夹
mv source_flie dest_file #将source_file 移动到dest_file 的位置
find ./ | wc -l  #查看当前目录下文件的个数
cp -r source_dir dest_dir #将source_dir的内容拷贝到dest_dir
```

### 目录切换

```sh
cd {diretctory}#切换到文件或者目录的位置
cd -          #切换到上一个工作目录
cd ~          #切换到home目录
pwd           #显示当前路径
path:$cd path #更改当前的工作路径
```

### 列出目录项

```sh
ls          #查看目录下的文件
ls -lrt     #查看文件并按时间排序
ls -al|more #查看文件的详细信息
ls -a       #查看隐藏文件
```

### 查找目录
```sh
find {diretctory} -name "nvidia*" | xargs file #查询文件或者是目录
find {diretctory} -name '*.md' #查找目标文件夹中是否有.md文件
find {diretctory} -name "*.md" -exec rm {} \; #递归当前目录及子目录删除所有.md文件
locate string #寻找包含string的路径
updatedb #更新locate路径数据库
```

### 查看文件内容
```sh
cat -n #显示时同时显示行号
ls -al |more #按页显示列表的内容
head -10 {file} #只看前10行
tail -5 {file} #只看文件的倒数第五行
diff {file1} {file2} #查看两个文件之间的区别
tail -f {file} #动态显示文本的最新信息
```

### 查找文件内容
```sh
egrep 'some_pattern' {file} #查找文件的内容
egrep 'some_pattern' {file} > out.txt #将查找的内容写入out.txt文件中
```
### 目录和文件权限修改
```sh
chown #改变文件拥有者
chmod #改变文件的读写执行等属性
chmod -R #递归修改子目录
chmod a+x {script} #增加脚本的可执行权限
```

### 给文件添加别名
```sh
ln {file} {file_other_name}    #硬链接：删除一个，另一个还存在并能找到
ln -s {file} {file_other_name} #软链接：删除源，另一个无法使用
```
### 管道和重定向

```sh
| #批处理命令连接执行
; #串联
&& #连续执行，但必须前面执行成功
|| #连续执行，如果前面执行失败则执行后一条

:> file 清空文件
echo {bababa} >> file 将输出重定向到文件
```

### 设置环境变量
账户启动之后执行的是`.profile`文件，可以通过设置这个文件来设置自己的环境变量

安装的软件路径一般需要添加的path中
```sh
PATH =.....
```

## 文本处理

### find 文件查找等处理
```sh
find . \( -name "*.txt" -o -name "*.pdf" \) - print #查找txt和pdf文件
find . -regex ".*\(\.txt|\.pdf\)$" #查找txt和pdf文件
find . -iregex ".*\(\.txt|\.pdf\)$" #忽略大小写的查找
find . ! -name "*.txt" -print #查找非txt文本
find . -maxdepth 1 -type f #查找深度为1
find . -type d -print  #查找所有目录
#更多find 命令请参考man find
```
### 后续操作
```sh
find . -type f -name "*.swp" -delete #找到删除
find . -type f -name "*.swp" | xargs rm
find . -type f -user root -exec chown weber {} \; #{}表示所有匹配上的文件名
find . -type f -mtime +10 -name "*.txt" -exec cp {} OLD \;
```

### grep 文本搜索
grep 常用参数
 * -o 只输出匹配的文本行
 * -v 只输出没有匹配的文本行
 * -c 统计文件中包含文本的次数
 * -n 打印匹配的行号
 * -i 搜索时忽略大小写
 * -I 只打印文件名

 

