 -Dvtag=v_vod_material_ztc



面经参考<https://troywu0.gitbooks.io/interview/content/>

## 每日学习记录

### 2020.7.22  

看序列化 kryo protobuf差异，序列化底层实现

zookeeper的原理，面试题

~~算法leetcode54螺旋数组、字符串的全排列~~  

ICMP  PING

### 2020.7.23

新的需求：

**这个下面的都在lz-trend TrendService里**

1. 发布声音 **找不到**

2. 发布动态  sendForwardTrend         kafka producer:trendProducer

3. 分享声音动态  addVoiceTrend        kafka producer:trendProducer

4. 节目被分享  addProgramTrend       

5. 互动：

   回复评论 replyCommentTrend             trendCommentProducer

   点赞评论 likeOperationTrendComment

6. 节目被播放 **找不到**

7. 节目获得点赞 addProgramTrend

8. 。。。。找不到

### 2020.7.24

公司app debug版本使用方法。（踩坑）

- 下载debug测试版本apk，安装。
- 连接office wifi，修改手机wifi dns 为公司dns
- 扫码绑定灯塔迭代。（这样请求才会去灯塔）
- 登录的时候输入170以后的手机号，获取验证码。
- 去录播小工具里获取redis中的验证码，填入手机成功登录。

模拟用户手机号 17021312166

进入主播中心页面时，需要再次登录，这时要在debug设置中关闭实名认证，不然登录完会再次跳转到登录页面



## 面经收集

### 智力题

百度：140克沙子，2g和7g的砝码，称50g沙子，要求称的次数最少

​	方法1：2g和7g称出9g，9g+7g称出来16g(称两次)，16g+2g+7g+9g+16g=50g

​	方法2：

腾讯 字节：64匹马，8个赛道，如何最少次比赛确定跑的最快的4匹马？

<https://blog.csdn.net/weichi7549/article/details/107371789/>

10场或者11场比赛得出结果，最后这个判断是解题的精髓。



### 07.16

百度一面面经
什么是mvc
runtime
实习做过哪些项目
https是什么
ssl加密原理
tcp拥塞控制，滑动窗口
输入一个url之后发生了什么
dns具体讲讲
如何从服务器获取资源具体讲讲
常见状态码
转发和重定向
两个算法：
1，一个数组，把偶数放前面，奇数放后面，返回
2，删除单链表的倒数第k个节点

### 07.16 百度

![1594896231675](C:\Users\ADMINI~1\AppData\Local\Temp\1594896231675.png)

### 字节9面（微服务）

<https://www.nowcoder.com/discuss/453852?type=post&order=time&pos=&page=3&channel=1010&source_id=search_post>

### 快手面经

<https://www.nowcoder.com/discuss/426600?toCommentId=6170066>

## 算法

### 排序算法

稳定排序和不稳定排序：<https://www.cnblogs.com/codingmylife/archive/2012/10/21/2732980.html>

#### 快排

```java
public void quicksort(int[] nums ,int start, int end){

	if(start>=end) return;
	int i=start;
	int j =end;
	int privot =nums[start];
	while(i<j){
		while(i<j&&nums[j]>=privot){
			j--;
		}
		while(i<j&&nums[i]<=privot){
			i++;
		}
		if(i<j){
			swap(nums,i,j);
		}
	}
	nums[start]=nums[i];
	nums[i]=privot;
	quicksort(nums ,start, i-1);
	quicksort(nums ,i+1, end);
}

```

#### 归并排序

讲得非常不错的视频，参考https://www.bilibili.com/video/BV1Ax411U7Xx/

剑指Offer的51题 数组中的逆序对就是归并的思想，参考<https://www.nowcoder.com/questionTerminal/96bd6684e04a44eb80e6a68efc0ec6c5?f=discussion>

下面的题解是针对51题计算逆序对的，比归并排序就多了一行代码---计算cnt。

<span id="Offer51"></span>

```java
public class Solution {
    int cnt =0;
    public int InversePairs(int [] array) {
        if(array==null||array.length==0) return 0;
        InversePairs(array,0,array.length-1);
        return cnt;
    }
    
    public void InversePairs(int [] array,int start,int end) {
        if(start>=end) return;
        int mid =(start+end)>>1;
        InversePairs(array,start,mid);
        InversePairs(array,mid+1,end);
        merge(array,start,mid,end);
    }
    
    public void merge(int [] array,int start,int mid,int end) {
        int tmp[] =new int[end-start+1];
        int i=start;int j=mid+1;int k=0;
        while(i<=mid&&j<=end){
            if(array[i]<=array[j]){
                tmp[k++]=array[i++];
            }else{
                tmp[k++]=array[j++];
                //计数
                cnt=(cnt+mid-i+1)%1000000007;//核心代码 计算该次比较的逆序对个数
            }
        }
        while(i<=mid){
            tmp[k++]=array[i++];
        }
        while(j<=end){
            tmp[k++]=array[j++];
        }
        for(int p=start;p<=end;p++){
            array[p]=tmp[p-start];
        }
    }
}
```



### leetcode

#### K链表翻转

#### 39 组合总和

回溯+剪枝，为了剪枝，每次for循环不从0开始。

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> list =new ArrayList<>();
        ArrayDeque<Integer> deque =new ArrayDeque<>();
        Arrays.sort(candidates);
        dfs(candidates,candidates.length,0,target,list,deque);
        return list;
    }
    public void dfs(int[] arr,int n,int cur,int sum,List<List<Integer>> list,ArrayDeque<Integer> deque){
        if(sum==0){
            list.add(new ArrayList<>(deque));
            return;
        }
        for(int i=cur;i<n;i++){
            if(sum<0){
                return;
            }
            deque.add(arr[i]);
            dfs(arr,n,i,sum-arr[i],list,deque);
            deque.removeLast();
        }
    }
}
```



#### 46 全排列

全排列用dfs回溯求解。

```java
class Solution {
    List<List<Integer>> rslist =new ArrayList<>();
    List<Integer> list =new ArrayList<>();
    int n;
    int[] used;
    public List<List<Integer>> permute(int[] nums) {
        n=nums.length;
        used=new int[n];
        dfs(nums,0);
        return rslist;
    }
    public void dfs(int[] nums,int cur){
        if(cur==n){
            rslist.add(new ArrayList<>(list));
            return;
        }
        for(int i=0;i<n;i++){
            if(used[i]==0){
                used[i]=1;
                list.add(nums[i]);
                dfs(nums,cur+1);
                used[i]=0;
                list.remove(list.size()-1);
            }
        }
    }
}
```

#### 47 全排列2

这个题比上面46多了一个不可重复，在回溯的基础上要进行剪枝。

参考题解：<https://leetcode-cn.com/problems/permutations-ii/solution/hui-su-suan-fa-python-dai-ma-java-dai-ma-by-liwe-2/>

建议把ArrayList换成ArrayDeque，其实使用Stack就行，Java官方Stack类的建议是ArrayDeque。

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        int n =nums.length;
        int[] used =new int[n];
        List<List<Integer>> rslist =new ArrayList<>();
        List<Integer> list =new ArrayList<>();
        Arrays.sort(nums);//排序是剪枝的前提
        return dfs(nums,n,used,0,rslist,list);
    }
    public List<List<Integer>> dfs(int[] nums,int n,int[] used,int cur,List<List<Integer>> rslist,List<Integer> list){
        if(cur==n){
            rslist.add(new ArrayList<>(list));
            return rslist;
        }
        for(int i=0;i<n;i++){
            if(used[i]==1){
                continue;
            }
            if(i>0&&nums[i]==nums[i-1]&&used[i-1]==0){
                continue;
            }
            used[i]=1;
            list.add(nums[i]);
            dfs(nums,n,used,cur+1,rslist,list);
            used[i]=0;
            list.remove(list.size()-1);
        }
        return rslist;
    }
}
```

#### 54 螺旋矩阵

四个指针控制范围，向右，向下，向左，向上遍历，注意边界条件。

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> list =new ArrayList<>();
        if(matrix==null||matrix.length==0) return list;  
        int low =0;
        int high=matrix.length-1;
        int left=0;
        int right=matrix[0].length-1;
        while(left<=right&&low<=high){
            for(int i=left;i<=right;i++) list.add(matrix[low][i]);//向右

            for(int i=low+1;i<=high;i++) list.add(matrix[i][right]);//向下

            //向左  if判断防止low,high相等 重复遍历
            if(low<high){
                for(int i=right-1;i>=left;i--) list.add(matrix[high][i]);
            }
            //向上
            if(right>left){
                for(int i=high-1;i>low;i--) list.add(matrix[i][left]);//注意这里i=low位置已经再向右 的过程中被遍历了
            }
            left++;
            low++;
            right--;
            high--;
        }
        return list;
    }
}
```

64 最小路径和

简单dp，代码如下。

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int n =grid.length-1;
        int m=grid[0].length-1;
        int[][] dp =new int[n+1][m+1];

        dp[0][0]=grid[0][0];
        for(int i=1;i<=n;i++) dp[i][0]=dp[i-1][0]+grid[i][0];
        for(int j=1;j<=m;j++) dp[0][j]=dp[0][j-1]+grid[0][j];
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                dp[i][j]=Math.min(dp[i][j-1],dp[i-1][j])+grid[i][j];
            }
        }
        return dp[n][m];
    }
}
```



### 剑指Offer

#### [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

```java
class Solution {
    public String[] permutation(String s) {
        //全排列   剪枝需要条件判断
        char[] chars =s.toCharArray();
        int n =chars.length;
        int[] used =new int[n];
        List<String> rslist =new ArrayList<>();

        Arrays.sort(chars);//排序是剪枝的关键

        StringBuilder sb =new StringBuilder();
        dfs(chars,n,used,0,rslist,sb);
        return rslist.toArray(new String[0]);//list转数组  数组类型实例对象作为传参
    }
    public void dfs(char[] chars,int n,int[] used,int cur,List<String> rslist,StringBuilder sb){
        if(cur==n){
            rslist.add(sb.toString());
            return;
        }
        for(int i=0;i<n;i++){
            if(used[i]==1){
                continue;
            }
            if(i>0&&chars[i]==chars[i-1]&&used[i-1]==0){//剪枝关键
                continue;
            }
            used[i]=1;
            sb.append(chars[i]);
            dfs(chars,n,used,cur+1,rslist,sb);
            sb.deleteCharAt(sb.length()-1);
            used[i]=0;
        }
    } 
}
```



#### [剑指 Offer 51. 数组中的逆序对](#Offer51)



## Java基础

### Java8

- ThreadLocal.withInitial

- Stream流

  例子如下。

  定义一个Person类：

  ```java
  class Person{
      private String name;
      private int age;
      private int sex;//0女 1男
      public Person(String name, int age, int sex) {
          this.name = name;
          this.age = age;
          this.sex = sex;
      }
      public String getName() {
          return name;
      }
      public int getAge() {
          return age;
      }
      public int getSex() {
          return sex;
      }
  }
  ```

  创建集合，演示Stream流：

  ```java
  public static void main(String[] args) {
          List<Person> list =new ArrayList<>();

          list.add(new Person("张三",18,1));
          list.add(new Person("张三",18,1));
          list.add(new Person("李四",16,0));
          list.add(new Person("王五",15,1));
          list.add(new Person("赵六",21,0));
          list.add(new Person("孙七",10,1));

          //获取年龄大于18的女性的集合
          List<Person> list1 = list.stream()
                  .filter(item ->item.getAge()>18&&item.getSex()==1)//年龄大于18 女性
                  .distinct()//去重
                  .skip(1)//跳过n个元素
                  .limit(2)//限制结果个数
                  .collect(Collectors.toList());

          //遍历
          list.forEach(item->{
              System.out.println(item.getSex());
              System.out.println(item.getAge());
              System.out.println(item.getName());
          });

      }
  ```

  ​



### 序列化 kryo

<https://cloud.tencent.com/developer/article/1511793>

kryo使用指南 <https://blog.csdn.net/andong3791/article/details/101965131?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-5.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-5.nonecase>

序列化漫谈 <https://www.cnblogs.com/liouwei4083/p/6123383.html>

### 线程池

1. newSingleThreadExecutorl()

   只有一个线程，适合于任务顺序执行的场景，阻塞队列是LinkedBlockingQueue  无界队列

2. newcachedThreadPool()

   线程数量不固定，最大Integer.MAX_VALUE个，回收时间默认一分钟，任务队列为Synchronous 只能存放一个元素

3. newFixThreadPool()

   指定线程数量，linkedBlockingQueue 无界队列

   ​

4. newScheduleThreadPool()

   可在给定的延迟后运行，或者定期的执行

   线程数量不固定，DelayWorkQueue()，延时队列

底层都是new ThreadPoolExecutor(//参数)实例化得到的




#### 线程数量设置

cpu密集型  n+1

io密集型  2*n+1

以上只是经验取值

最佳线程数目 =（（线程等待时间+线程cpu时间）/线程cpu时间））*cpu数目

=（等待时间/cpu时间 +1）*cpu数目

## JVM

### jstack



### 如何排查OOM？

1. ps -aux| grep java查看一下java进程，找到对应进程的pid。
2. top 查看cpu、内存使用率，看%MEM这列，对应的进程是不是占用很高。
3. jstat -gcutil pid 1000 10，用jstat工具对指定pid的进程查看新生代老年代内存使用率，young gc和full gc的次数，1000ms打印一次，一共打印10次。
4. jmap -histo pid打印出当前堆中所有每个类的实例数量和内存占用
5. jmap -dump:format=b,file=文件名 [pid]，把指定java进程的堆内存快照dump到指定的文件进行快照分析





### GC ROOTS

虚拟机栈（栈帧中的本地变量表）中引用的对象；本地方法栈JNI中的引用对象；方法区中的类静态属性引用的对象；方法区中常量引用的对象。

### 类加载过程

类的加载过程：加载->连接->初始化

连接分为三个步骤：验证->准备->解析

参考：<https://www.cnblogs.com/ityouknow/p/5603287.html>

为什么要破坏双亲委派类加载机制？

参考：<https://blog.csdn.net/majianxin1/article/details/102604237?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase>

## IO

#### Netty

三个优点：

1. 高并发，基于NIO开发的网络通信框架，对比BIO并发性能提升了很多。
2. 传输快，传输基于零拷贝实现，减少不必要的内存拷贝，传输效率高
3. 封装好，封装了NIO的很多操作细节，提供了易用的接口调用

##### Netty的零拷贝

**传统意义的零拷贝**

mmap和sendFile <https://www.jianshu.com/p/275602182f39>

DMA (Direct Memory Access)直接存储访问

```java
File file = new File("index.html");
RandomAccessFile raf = new RandomAccessFile(file, "rw");

byte[] arr = new byte[(int) file.length()];
raf.read(arr);

Socket socket = new ServerSocket(8080).accept();
socket.getOutputStream().write(arr);
```

上面的代码是一段网络通信代码。我们会调用 read 方法读取 index.html 的内容—— 变成字节数组，然后调用 write 方法，将 index.html 字节流写到 socket 中，那么，我们调用这两个方法，在 OS 底层发生了什么呢？我这里借鉴了一张其他文字的图片，尝试解释这个过程。上半部分表示用户态和内核态的上下文切换。下半部分表示数据复制操作。

![img](https://upload-images.jianshu.io/upload_images/4236553-174b8d9cc6119e67.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

1. 首先read调用，用户态切换到内核态，DMA读取磁盘文件的数据拷贝到内核的缓冲区。
2. 内核缓冲区的数据拷贝到用户缓冲区，同时发生内核态到用户态上下文切换。
3. write调用，用户缓冲区数据拷贝到socket缓冲区，同时用户态到内核态上下文切换。
4. 数据异步的从socket缓冲区使用DMA引擎拷贝到网络协议引擎。这里不用上下文切换。

Linux 2.1 版本 提供了 sendFile 函数，其基本原理如下：数据根本不经过用户态，直接从内核缓冲区进入到 Socket Buffer，同时，由于和用户态完全无关，就减少了一次上下文切换。

Linux 在 2.4 版本中，做了一些修改，避免了从内核缓冲区拷贝到 Socket buffer 的操作，直接拷贝到协议栈，从而再一次减少了数据拷贝。如下图。

![img](https://upload-images.jianshu.io/upload_images/4236553-00c3e47936ecea25.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

netty的零拷贝：

1. 接收和发送ByteBuffer采用对外直接内存，不需要进行字节缓冲区的二次拷贝。传统堆内存读写socket要将堆内存的Buffer拷贝一份到直接内存，然后再写入socket。
2. 提供了组合Buffer对象，可以聚合多个ByteBuffer对象，用户可以像操作一个ByteBuffer一样操作组合的ByteBuffer，避免了传统通过内存拷贝的方式将几个小的Buffer组合成大的Buffer
3. 文件传输采用了transferTo方法，底层调用操作系统的sendFile()直接将内核文件缓冲区数据发送到目标channel，避免了传统的通过循环write的方式导致无用的内存拷贝。


## 数据库

建议阅读	MySQL是怎样运行的：从根儿上理解MySQL

需要了解的知识点

```shell
一、MySQL InnoDB 存储原理深入剖析
    MySQL记录存储
    页头
    虚记录
    记录堆
    自由空间链表
    未分配空间
    Slot 区
    页尾
    业内记录维护
    顺序保证
    插入策略
    页内查询
二、MySQL InnoDB 索引实现原理及主键设计选择分析
    聚簇索引
    二级索引
    联合索引
    主键选择分析
三、MySQL InnoDB 存储引擎内存管理
    Buffer Pool
    Page
    Free list
    Flush list
    Page Hash 表
    LRU
四、MySQL InnoDB 存储引擎事务实现原理
    MySQL 事务基本概念
    事务特性
    并发问题
    隔离级别
    MySQL 事务实现原理
    MVCC
    undo log
    redo log
```

### SQL题

成绩表，三个字段：姓名、课程、成绩，求课程平均成绩大于85的学生姓名和平均成绩

```SQL
select n , sc from (select avg(score) as sc,name as n from tb group by n having sc>85 ) 
```

### 联合索引

联合索引的结构 <https://blog.csdn.net/ibigboy/article/details/104571930?depth_1->

### 说说索引优化

- 对常用作为条件查询的字段建立索引。

- 尽量不使用长字符串做索引，占用空间巨大。

- 按照联合索引的最左匹配原则编写SQL。

- mysql5.6以后可以 开启索引下推，减少存储引擎返回的数据量，将数据的条件筛选在引擎端完成。<https://www.cnblogs.com/Chenjiabing/p/12600926.html>

  可以减少存储引擎查询基础表的次数，也可以减少MYSQL服务器从存储引擎接收数据的次数。

- 开启mrr，将随机io优化成为顺序io，对于机械硬盘会提升很大性能。

### Buffer Pool

默认大小为128M，可通过innodb_buffer_pool_size配置。

buffer pool中的缓存页大小为16KB，每个缓存页都包含控制信息，

### join的执行过程



## Linux

### 指令 

#### 利用grep打印匹配的上下几行

如果在只是想匹配模式的上下几行，grep可以实现。

```shell
$grep -5 'parttern' inputfile //打印匹配行的前后5行

$grep -C 5 'parttern' inputfile //打印匹配行的前后5行

$grep -A 5 'parttern' inputfile //打印匹配行的后5行

$grep -B 5 'parttern' inputfile //打印匹配行的前5行
```


查看mysql慢日志中ip地址为192.168.0.10发送过来的SQL语句的后面三行

```shell
tail -50 /usr/local/mysql/data/sql-slow.log |grep -3 '192.168.0.10'  
```

匹配php错误日志中某一个字段

```shell
tail -100 /data/logs/php/php_error_5.3.log  | grep  "Memcache::get()";
```

查看某一个文件第5行和第10行

```shell
 sed -n '5,10p' filename 
```

这样你就可以只查看文件的第5行到第10行。

#### 查看端口是否被占用

netstat -anp | grep 端口号

## 操作系统

虚拟内存和物理内存的映射关系和工作原理：

<https://blog.csdn.net/don_chiang709/article/details/89087709>

#### 进程通信：

1. 信号

   进程通过信号进行通信，用于用纸接受进程的某个事件已经发生。如kill -9 pid 就是向pid进程发起结束进程的信号

2. 管道。有名管道和匿名管道。匿名管道用于 父子进程的通信，而有名管道用于 无亲缘关系的进程通信，

## 计算机网络

### HTTPS

**优缺点**

优点：

http+ssl构建，可加密传输和身份认证，安全性高。

虽然不是绝对安全，但是大幅增加了中间人攻击的成本。

缺点：

https握手阶段比较费时。

缓存不如http高效。

SSL证书需要收费。

SSL证书需要绑定IP，不能在同一个ip绑定多个域名，ipv4资源支持不了这种消耗。

--------------------------------------------

**加密机制**

采用混合加密机制。在交换密钥环节使用公开密钥加密方式，之后的建立通信交换报文阶段则使用共享密钥加密。HTTPS 在内容传输的加密上使用的是对称加密，非对称加密只作用在证书验证阶段。

**证书**

遗憾的是，仅凭借公开密钥加密的方式是不够的，因为无法证明公钥本身是真实的公钥，存在被伪造的隐患。为解决上述问题，使用数字证书机构CA 颁发的公钥证书，CA处于客户端和服务端都可以信赖的第三方机构的立场上。

**通信过程**

客户使用https的URL访问Web服务器，要求与Web服务器建立SSL连接。

Web服务器收到客户端请求后，会将网站的证书信息（证书中包含公钥）传送一份给客户端。

客户端的浏览器与Web服务器开始协商SSL/TLS连接的安全等级，也就是信息加密的等级。

客户端的浏览器根据双方同意的安全等级，建立会话密钥，然后利用网站的公钥将会话密钥加密，并传送给网站。

Web服务器利用自己的私钥解密出会话密钥。

Web服务器利用会话密钥加密与客户端之间的通信。

参考：

<https://blog.csdn.net/weixin_46124214/article/details/105875458>

### 网络协议分层

**OSI七层模型**

OSI中的层            功能                                                        TCP/IP协议族 
应用层                 文件传输，电子邮件，文件服务，虚拟终端         TFTP，HTTP，SNMP，FTP，SMTP，DNS，Telnet 
表示层                 数据格式化，代码转换，数据加密                                    没有协议 
会话 层                 解除或建立与别的接点的联系                                          没有协议 
传输层                 提供端对端的接口                                                        TCP，UDP （RTP）
网 络层                 为数据包选择路由                                                        IP，ICMP，RIP，OSPF，BGP，IGMP 
数据链路层           传输有地址的帧以及错误检测功能                            SLIP，CSLIP，PPP，ARP，RARP，MTU 
物 理层                 以二进制数据形式在物理媒体上传输数据                             ISO2110，IEEE802，IEEE802.2

**TCP/IP五层模型的协议**

应用层 
传输层：四层交换机、也有工作在四层的路由器

网络层：路由器、三层交换机

数据链路层：网桥（现已很少使用）、以太网交换机（二层交换机）、网卡（其实网卡是一半工作在物理层、一半工作在数据链路层）

物理层：中继器、集线器、还有我们通常说的双绞线也工作在物理层

### DNS

详解DNS: <https://zhuanlan.zhihu.com/p/79350395>

DNS用到UDP和TCP，**域名解析**使用UDP，简单，速度快，只要一个请求一个应答即可。但是UDP传输不超过512字节，不过DNS查询域名一般返回内容都不超过512字节。区域传送使用TCP，



### ICMP

ICMP全称是Internet Control Message Protocol，即互联网控制报文协议。

ICMP报文是封装在IP包里面的，工作在网络层，是IP协议的助手。

ICMP的报文种类有两种：差错报告报文、查询报文。

报文格式包括1个字节的类型，1个字节的code代码，2个字节的校验和，长度可变的数据。

差错报告报文包括：目的不可达、源主机消亡、超时、参数问题、重定向。查询报文包括：回应请求和应答、信息请求和应答（已弃用）、时间戳和时间戳应答、地址掩码请求和应答、路由器通告和请求。

参考：<https://www.cnblogs.com/ccsccs/articles/4224441.html>

### PING

ping是基于ICMP协议工作的，参考文章

<https://www.cnblogs.com/xiaolincoding/archive/2020/03/25/12571184.html>

1.首先查本地arp cache信息，看是否有对方的mac地址和IP地址映射条目记录
2.如果没有，则发起一个arp请求广播包，等待对方告知具体的mac地址
3.收到arp响应包之后，获得某个IP对应的具体mac地址，有了物理地址之后才可以开始通信了,同时对ip-mac地址做一个本地cache
4.发出icmp echo request包，收到icmp  echo reply包

## 中间件

### Redis

#### 淘汰策略

1. noeviction  不会继续服务写请求
2. volatile-lru 最少使用的key被淘汰（只针对设置了过期时间的key）
3. volatile-ttl 淘汰ttl最小的key
4. volatile-random 淘汰过期key集合中的随机的key

####  volatile策略只会针对带过期时间的 key 进行淘汰

5. allkeys-lru  同 volatile-lru，但是 key 针对是全体的 key 集合。
6. allkeys-random 同 volatile-random，但是 key 针对是全体的 key 集合。

### Dubbo(RPC)

#### 负载均衡（4种实现）

官网文档：<http://dubbo.apache.org/zh-cn/docs/source_code_guide/loadbalance.html>

1. 基于权重随机算法的RandomLoadBalance。   按照权重值进行均匀随机分配。

2. 基于最小活跃调用数算法的LeastActiveLoadBalance。 所有服务提供者初始活跃数为0，收到请求+1，处理完请求-1.再服务运行一段时间后，如果某个服务提供者活跃调用数越少，表明该服务提供者效率越高，单位时间内可处理的请求更多。

3. 基于加权轮询算法的RoundRobinLoadBalance。按权重比例分配请求数量。

   如A,B,C权重为[2,5,1]  则8次请求的顺序是 A B C A B B B B，即轮询+加权

4. 基于hash一致性算法的ConsistentHashLoadBalance。根据 ip 或者其他的信息为缓存节点生成一个 hash，并将这个 hash 投射到 [0, 2^32 - 1] 的圆环上。当有查询或写入请求时，则为缓存项的 key 生成一个 hash 值。然后查找第一个大于或等于该 hash 值的缓存节点。

   ​



### Kafka

**如何防止重复消费？**

1. 同步提交，会有性能影响。
2. 消息使用唯一id标识-->落表（主键或者唯一索引避免重复）或者选择唯一主键存储到redis，若存在则不处理，不存在则插入后处理。

**如何防止消息丢失？**

1. 生产者丢失-->使用producer.send(msg,callback)回调机制获取消息是否发送成功，未成功则重试。
2. 消费者丢失-->先消费消息，再更新offset。防止offset更新没有消费完成导致丢失。

### Zookeeper

#### CAP理论

CAP:cap consistency一致性，availablity可用性，分区容错性partion tolerance。

zookeeper保证了CP，牺牲了A，防止脑裂时，分布式系统的不一致性。而Eureka保证了AP牺牲了C，保证高可用。ZAB 协议是 CAP 理论中 CP 的典型实现，其崩溃恢复阶段涉及到的 Leader 节点选举过程和数据同步选举完成后的数据同步过程都是对外不提供服务的，就是为了保证数据的强一致性牺牲了可用性。

#### zookeeper核心知识

<https://www.cnblogs.com/wlwl/p/10715065.html>

zookeeper角色：observer处理读请求，没有投票和选举权。follower处理读请求，leader会根据算法落实到某个follower节点。leader一个集群只有一个，处理写请求，负责发起投票和决议，更新系统状态。每次写请求都会发起投票，只有过半的节点通过才能写入数据。

zookeeper客户端与服务端建立连接会创建session，通过心跳机制来确定session是否过期，如果过期，该客户端的临时节点都会失效。

#### 为什么不推荐zookeeper做注册中心？阿里技术文章

<http://jm.taobao.org/2018/06/13/%E5%81%9A%E6%9C%8D%E5%8A%A1%E5%8F%91%E7%8E%B0%EF%BC%9F/>

#### Zookeeper如何保证数据的一致性？

<<https://www.cnblogs.com/tkzL/p/12916116.html>>

通过Zab（原子广播）协议保证分布式事务的最终一致性。

Zab协议分为三部分：

1. - **消息广播阶段**

   1. 一个事务请求（Write)进来，Leader会把写请求包装成Proposal事务，并添加一个全局唯一的64位递增事务ID---Zxid。
   2. Leader广播Proposal事务，将Proposal事务发送到为每个Follower节点单独分配的FIFO队列中。
   3. Follower收到Proposal后持久化到磁盘，返回ACK。
   4. Leader收到超过半数的Follower的ACK后（Quorum机制），提交本地机器上的事务，同时开始广播commit，Follower节点收到commit之后，完成各自的事务提交。

   ZAB 协议针对事务请求的处理过程类似于一个两阶段提交过程，第一阶段是广播事务操作，第二阶段是广播提交操作，而在这种两阶段提交模型下，是无法处理因 Leader 节点宕机带来的数据不一致问题的，比如下面两种情况：

   1. 当 Leader（Server1） 发起一个事务 Proposal1 后就宕机了，导致 Follower 都没有 Proposal1。
   2. 当 Leader 发起 Proposal2 后收到了半数以上的 Follower 的 ACK，但是还没来得及向 Follower 节点发送 Commit 消息就宕机了。

   **为了解决 Leader 宕机以及宕机后导致的数据不一致问题，ZAB 协议引入了崩溃恢复模式。**

   崩溃恢复模式必须解决以下问题：

   1. Server1 恢复过来再次加入到集群中的时候，必须确保丢弃 Proposal1，即保证被丢弃的消息不能再次出现。
   2. 选举出的新 Leader 必须拥有集群中所有机器 Zxid 最大的 Proposal，即保证已经被处理的消息不能丢。

2. - **崩溃恢复阶段**

   > Zookeeper 集群进入崩溃恢复阶段的时机：
   >
   > - 集群服务刚启动时进入崩溃恢复阶段选取 Leader 节点。
   > - Leader 节点突然宕机或者由于网络原因导致 Leader 节点与过半的 Follower 失去了联系，集群也会进入崩溃恢复模式。

    	选举Leader节点

    - 1. 各个节点变为Looking状态

         Leader宕机后，各个Follower节点状态变更为Looking，参与Leader选举过程。Observer不参与。

      2. 各个Server节点发起投票

         第一次投票所有的节点都会投自己，然后各自将投票发送给集群中的所有机器。

      3. 集群接收各个服务器的投票，处理投票和选举

         判断的依据如下：首先选举 epoch 最大的，如果 epoch 相等，则选 zxid 最大的，若 epoch 和 zxid 都相等，则选择 server id 最大的。在选举过程中，如果有节点获得超过半数的投票数，则会成为 Leader 节点，反之则重新投票选举。

      4. 选举成功，各自的节点状态为Leading和Following。

   - 数据同步

     崩溃恢复完成选举以后，接下来的工作就是数据同步，在选举过程中，通过投票已经确认 Leader 节点是最大 Zxid 的节点，同步阶段就是利用 Leader 前一阶段获得的最新 Proposal 历史同步集群中所有的副本。