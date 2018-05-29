# Linux 实战
### 字符输出
```
cat /proc/$PID/environ 查看运行时环境变量
使用tee同事保留输出到文件和控制台  cat a* | tee out.txt|cat  -n
使用exec创建文件描述符
cmd;$?返回上一个命令的结果 成功返回0
read 读取指令
read -n var
IFS(Internal Field Separator)
字符串比较用[[$str1 == $str2]]
```
### shell中的逻辑控制
```
循环写法:
for item in {1..50}
do
echo $item;
done

while condition
do 
commands;
done

x=0;
until [$x -eq 9];
do let x++;
echo $x;
done

比较控制：
if conditon;
then
commands;
elif condition;
then
    commands;
else
    commands;
fi
```
### 常用命令
#### find 用法实战
```
find . -name "*.txt" -print
find . \( -name "*.txt" -o -name "*.pdf" \) -print
find . -regex ".*\(\.py|\.sh\)$"
find . -maxdepth 1 -type f -print
find . -type d -print
find . -type f -amin -70 #通过时间来查找文件
find . -type f -size +2k
find . -type f -perm 644
find . -name "*.c" -exec cat {} \; >all_c_files.txt #强大的 exec {}代表找到的文件
```
#### xargs

```
cat example.txt | xargs -n 3
cat args.txt | xargs -I {} ./cecho.sh -p 
```
#### tr

```
echo "HEELO WORLD" | tr 'A-X' 'a-z'
echo "Hello 123 world 456" | tr -d '0-9'
```
#### 校验与核实
```
md5sum sha1sum
```
#### 排序与唯一
```
sort -nrk 1 data.txt 以第一列数字倒叙排序
uniq sorted.txt
sort unsorted.txt | uniq -c #统计出现的次数
sort unsorted.txt | uniq -d #找出文件中重复的行
```
#### 分割文件和数据
```
split -b 10k data.file -d -a 4 split_file #以split_file为前缀 4个数字作为文件名字
```
#### 提取文件名以及文件后缀
```
file_jpg="sample.jpg"
name=${file_jpg%.*}
extension=${file_jpg#*.}
```
### 以文件之名
```
dd if=/dev/zero of=junk.data bs=1M count=1 #生成1M大小的junk.data文件，内容都是0
comm A.sorted.txt B.sorted.txt #比较A,B两个文件
mkdir -p /a/b/c/d
chown user.group filename #改变文件所有权
chmod a+t directory_name #设置粘置位
chmod 777 . -R #以递归形式改变权限
chown user.group . -R #改变所有权
chattr +i file #将文件设置成不可修改
ln -s target symbolic_link_name #创建符号链接
readlink symbolic_link_name #查看符号链接
diff -u version1.txt version2.txt > version.patch #查看文件差异并把差异写到version.patch文件中
seq 11 | head -n 5 #打印前5行
seq 11 | tail -n 5 #打印后5行
ls -d */ #列出当前目录
利用pushd popd cd -来切换目录
wc -l file # 统计行数
wc -w file # 统计单词数
wc -c file # 统计字符数
tree path -P PATTERN #用通配符找出符合的样式
tree path -I PATTERN #找出非通配符的样式
```
### 让文本飞
```
grep "" filename # 在文本中找到匹配的文字
grep -E "[a-z]09" filename #在文本中找到匹配正则的字符串
grep -v match_pattern file #打印除包含match_pattern行以外的行
grep -c match_pattern file #对match_pattern进行次数统计
grep -n match_pattern file #打印所匹配字符的行数
grep "text" . -R -n #对文本进行递归搜索
echo hello world | grep -i "HELLO" #忽略大小写
grep -e "pattern1" -e "pattern2" #匹配多个正则表达式
seq 10 | grep 5 -A/B/C 3 # 打印找到行-之前/-之后/-前后 3行
cut -f2,3 -d";" data.txt #打印文件的第2，3列 列的分隔符是; 默认是空格
sed '/^$/d' file #移除空白行
echo this is an example | sed 's/\w\+/[&]/g'
awk 'BEGIN {statement} {statement} END {statement}'
echo -e "line1\nline2" | awk 'BEGIN{ print "start" }{print}END{print "END"}'
```
### 网络
```
wget url -O download.img -o log
curl --referer Referer_URL target_URL
curl url --cookie "a=b;c=d"
curl url --coolie-jar cookie_file
curl -u user:pwd url
curl -I https://www.baidu.com #获取所有头部信息
curl --data "name=value" URL -o output.html #发送post请求
wget URL -post-data "name=value" URL
nslookup
host
lsof
netstat
```
### 文件归档，压缩
```
tar -cf output.tar file1 file2 file3 folder1 #-c 代表创建文件 -f 指定文件名
tar -rvf original.tar new_file #向已存在的归档文件添加一个文件
tar -tf archive.tar #查看归档文件的内容
tar -xf archive.tar #将归档文件中的内容提取到当前文件
tar -f archive.tar --delete file1 file2 #从给定的归档文件中删除文件
tar -czvfa archive.tar.gz file #归档并压缩
zcat #无需解压读取压缩文件内容
```
### 磁盘
```
du -h file
du -m  file
```
### 管理
```
which #打出cmd在path所在位置
whereis #不仅打出位置 还包括使用手册的位置
uptime
cat /proc/cpuinfo 
crontab -l -u user
```