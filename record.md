-Dvtag=v_dianbo_modifytopic

-Dvtag=v_lizhi_pushGuide_20200812

力扣待做    

1312  字符串转回文串的最少插入次数   

72 字符串1转字符串2 的最少操作次数

根据前序和中序复原二叉树

二叉树转双向链表





## 软件下载地址

### mysql:

中科大镜像 <http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-8.0/mysql-8.0.16-winx64.zip>

搜狐镜像 <http://mirrors.sohu.com/mysql/MySQL-8.0/>

### python:

淘宝镜像 <http://npm.taobao.org/mirrors/python>





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

模拟用户手机号 **17021312166**

用户id 5124103437373412396

波段号 13418335

进入主播中心页面时，需要再次登录，这时要在debug设置中关闭实名认证，不然登录完会再次跳转到登录页面

### 2020.7.28

前缀树

用户动态触发 kafka消息 test

分享声音到：

荔枝动态

msg: v_dianbo_mission!%#clientIp:192.168.10.33,producerIp:172.18.10.218,bizEnv:lizhi!%#{"platform":29,"time":1595920857430,"userId":5124103437373412396,"voiceId":2801883327137716742,"voiceUserId":2639561500921979948}

QQ

msg: v_dianbo_mission!%#clientIp:192.168.10.33,producerIp:172.18.10.218,bizEnv:lizhi!%#{"content":"测试_51","platform":24,"time":1595920905458,"userId":5124103437373412396,"voiceId":2801883327137716742,"voiceUserId":2639561500921979948}

### 2020.7.29

广联达笔试

第一题小顶堆排序求解。

第二题第二题就是给一个序列，只能用一种操作---令x为最小的有重复的数字，删除从左数的第一个x，把第二个变为2*x，一直这样操作，得到最终序列是什么。

Map保存元素和索引，while循环一直找Map中存在等于当前值的数，修改对应索引的值。

第三题给n个数，最多是m位二进制，m小于20，然后a&b=b，表示数a能包含数b，然后把这些数分堆，每堆只能有一个底座（也就是a&b=b的a），求这些数最少有几个这样的a就能把所有数都放在底座上（只要满足关系就行。。），然后还有个特殊，就是可以有一次操作，操作位把某个数的某个二进制位的数变换一下，就是求最少的堆个数。

不会做。。。

### 2020.7.30

操作系统 段页管理机制

leetcode 337 11 111

### 2020.7.31

运营后台发布兑换商品，消费钻石兑换商品，后台审核通过发送kafka消息。

消费钻石的kafka消息

msg: v_dianbo_mission!%#clientIp:192.168.18.106,producerIp:172.18.20.23,bizEnv:lizhi!%#{"diamondCount":10,"recordType":1,"time":1596181279985,"userId":5124103437373412396

leetcode刷题 

线程池    bean生命周期



value = common!%#clientIp:172.18.10.218,producerIp:172.18.10.218,bizEnv:lizhi!%#{"clientVersion":147680,"deviceId":"N_61ceb8e6dfe53213","incrCount":1,"ip":"192.168.10.34","platform":"Android 29","playType":0,"source":"","uid":5124103437373412396,"voiceId":2499935976722270214,"voiceUserId":2571481447246544428})

### 2020.8.2

主播任务系统条件

预发上线的项目： 

​	lz_vod_anchor_center_pre

​	lz_voice_pre

​	lz_vod_comment_pre

git fetch和pull详解 <https://www.cnblogs.com/runnerjack/p/9342362.html>

### 2020.8.5

零钱兑换1，2 

<https://leetcode-cn.com/problems/coin-change-2/solution/ling-qian-dui-huan-iihe-pa-lou-ti-wen-ti-dao-di-yo/>

push开关需求

根据设备id做判断，一天只展示一次。

定义一个类记录设备的状态，放在redis里。

包含字段 type当前状态，isTodayOpen今日是否打开过，上次??????

Type记录用户在哪个时间点状态，

key:设备id  value:type  

客户端可能会有两次请求的，第一次是用户打开相关界面时，请求判断是否弹窗提示。如果有提示，第二次是用户关闭界面时，请求改变type状态。

客户端每次请求的时候，携带通知开关的状态，如果开关是on=0，删除redis，return 提示=1。如果开关是off=1，这时对设备id对应的type类型进行判断，是否  return 提示=0或1

//0-    

0-关闭，还未提示，需要第一次提示  状态变为1

1-关闭，已经提示了一次，需要第二次提示 ， ，多一个字段 记录时间   状态变为2   延后五天

2-关闭，已经提示了两次，延后的五天到了， 状态变为3

3-关闭，，需要第三次提示 状态变为4

4-关闭，提示了三次，需要第四次提示，需要延后30天，时间字段记录30天延后 状态变为 0

**天、五天、30天均可配置**

如果

type =0  

=1



判断是否打开开关

### 2020.8.6

K个有序链表合并（递归和遍历） K个节点反转链表

今日任务：技术方案+开发基本功能     

主播任务系统条件  代码合并主分支 上线

任务：后台-push开关接口dc

~~服务端打点：1.下发push   2.显示小红点  已登录报uid未登录设备id~~

记得注意的点：

1. redis申请namespace 
2. redis过期时间配置 apollo
3. 文案配置 apollo
4. ~~as端的response和request在哪里配~~

### 8.7

发布接口   mvn clean deploy -Dmaven.test.skip=true -Dlz.env=online

代码规范  switch中的default必须写

~~最近公共父节点~~

BIO/NIO/AIO

Nagle算法  Netty

服务降级  限流  计数器算法  令牌桶算法



-Dconf.env=test -Dconf.key=lz-vod-whitelist -Dapp.name=lz-vod-whitelist

-Dconf.env=test -Dconf.key=app_vod_sundry -Dapp.name=app_vod_sundry

看网络部分<https://wenjie.store/archives/%E8%85%BE%E8%AE%AF2020%E5%B9%B46%E6%9C%88%E5%87%89%E7%BB%8F?token=496ec87ac07d41e281a2ee73dbf77dce>

### 8.11

redis问题 :写redis发现key  ttl查询为-1

解决：查看代码发现

```java
timeUnit =  24 * 3600 * 1000;
//.....省略代码
long expireTime = (long) 36 * timeUnit ;
```

时间类型 int*int超过了int上限，溢出变成负数了，使用long进行接收 ，同时对整型的运算进行强制转换。

### 8.17

1. ~~position  从1开始，有没有限制范围？~~  对
2. ~~channelId是不是应该为integer类型，数据库中是bitint对应long~~  没关系
3. ~~模块内容中的   声音==节目吗？~~  对
4. ~~选中【分类页】时，在右侧出现选择分类下拉框，可选择实际要跳转的所有一级分类（由服务端下发）  返回的内容是分类页的id吗？~~ 对
5. ~~url存储的时候要进行处理吗？~~


接口测试用例

```java
{
  "id":"5128885462689122431",
  "channelId": 20100,
  "name": "asww",
  "position": 1,
  "hasMore": 1,
  "moreActionType": 86,
  "moreActionContent": "20100",
  "contentType": 0,
  "num": 3,
  "contentList": [
    {
        "id":"5128917805940342911",
      "position": 2,
      "targetId": "2822707111228610566",
      "coverUrl": "http://521110.com"
    },
    {
        "id":"5128917805940343423",
      "position": 3,
      "targetId": "2822707111228610566",
      "coverUrl": "http://5223230.com"
    },
    {
        "id":"5128917805940343935",
      "position": 4,
      "targetId": "2822707111228610566",
      "coverUrl": "http://52444440.com"
    }
  ],
  "status": 0,
  "showStatus": 0
}
```

### 8.20

两个子节点的最近公共父节点

### 8.21

springboot自动装配原理

springboot启动过程

### 8.31

今日shopee面试未答出来的：

1. head和get。
2. csrf攻击
3. cpu多级缓存
4. （群主的问题）spring bean的作用域

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

## 算法+数据结构

### 二分法模板

<https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/>

### dijkstra算法

<https://www.zhihu.com/question/20630094/answer/758191548>

### 杂题

#### 高效判断一个数是否素数

<https://blog.csdn.net/qq_33945246/article/details/103045738>

关键是掌握质数分布的规律：大于等于 5 的质数一定和 6 的倍数相邻。例如 5 和 7，11 和 13,17 和 19 等等；

证明：令 x≥1，将大于等于 5 的自然数表示如下：
······ 6x-1，6x，6x+1，6x+2，6x+3，6x+4，6x+5，6(x+1），6(x+1)+1 ······
可以看到，不在 6 的倍数两侧，即 6x 两侧的数为 6x+2，6x+3，6x+4，由于 2 (3x+1)，3 (2x+1)，2 (3x+2)，所以它们一定不是素数，再除去 6x 本身，显然，素数要出现只可能出现在 6x 的相邻两侧。

所以循环的步长可以设为 6，然后每次只判断 6 两侧的数即可。

```java
 /**
     * 判断n是否素数
     */
    //解法1 暴力
    public boolean isPrimeNumber1(int n) {
        if (n < 2) return false;

        if (n == 2) return true;
        for (int i = 2; i < n; i++) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }

    //解法2 sqrt(n)
    public boolean isPrimeNumber2(int n) {
        if (n < 2) return false;
        if (n == 2) return true;
        int sqrt = (int) Math.sqrt(n);
        for (int i = 2; i <= sqrt; i++) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }

    //解法3 找到规律==> 大于等于 5 的素数一定和 6 的倍数相邻。但是和6的倍数相邻的数不一定是素数。因为合数总是可以写成素数的乘积，那么我们直接用n去除以质数就可以达到很好地优化目的。
    public boolean isPrimeNumber3(int n) {
        if (n < 5) {
            return n == 2 || n == 3;
        }
        if (n % 6 != 1 && n % 6 != 5) {
            return false;
        }
        int sqrt = (int) Math.sqrt(n);
        for (int i = 5;i<=sqrt;i++){
            if(n%i==0||n%(i+2)==0){
                return false;
            }
        }
        return true;
    }
```



#### IP地址和字符串互转

参考<https://blog.csdn.net/zhao_liwei/article/details/51853434>

#### 生产者消费者模型代码

参考：<https://baijiahao.baidu.com/s?id=1651415806527193535&wfr=spider&for=pc>

实现方式有两种：

方法一：借助阻塞队列，生产者put，当队列满，put线程阻塞。消费者take，当队列空，take线程阻塞。

首先定义消息结构Message。

```java
public class Message {
    private String msg;
    private int code;
    //.....

    public Message(String msg, int code) {
        this.msg = msg;
        this.code = code;
    }

    public String getMsg() {
        return msg;
    }

    public int getCode() {
        return code;
    }
}
```

编写生产者代码。

```java
public class Producer extends Thread {
    private final BlockingQueue<Message> queue;
    public Producer(BlockingQueue<Message> queue){
        this.queue=queue;
    }
    @Override
    public void run() {
        for(int i=0;i<10;i++){//模拟生产消息
            try {
                queue.put(new Message(Thread.currentThread().getName()+i,0));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }
}
```

编写消费者代码，并且编写main函数运行测试。

```java
public class Consumer extends Thread{
    private final BlockingQueue<Message> queue;
    public Consumer(BlockingQueue<Message> queue){
        this.queue=queue;
    }

    @Override
    public void run() {
        while(true){
            try {
                Message msg = queue.take();
                System.out.println("code: "+msg.getCode()+" msg: "+msg.getMsg());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        LinkedBlockingQueue<Message> messages = new LinkedBlockingQueue<>(10);//队列大小
        Thread producer =new Producer(messages);
        Thread consumer =new Consumer(messages);

        producer.start();//启动生产线程
        consumer.start();//启动消费线程

        System.out.println();
    }
}
```

方法二：普通队列，借助wait()和notify()机制

生产者

```java
public class Producer extends Thread {
    private Queue<Message> queue;
    private int size;
    public Producer(Queue<Message> queue,int size){
        this.queue=queue;
        this.size=size;
    }

    @Override
    public void run() {
        while (true){
            synchronized (queue) {
                while (queue.size() >= size) {
                    System.out.println("队列已经达到上限");
                    try {
                        queue.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                queue.add(new Message(Thread.currentThread() + UUID.randomUUID().toString().substring(0, 3), 0));
            }
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

```

消费者和main函数

```java
public class Consumer extends Thread{
    private Queue<Message> queue;

    public Consumer(Queue<Message> queue){
        this.queue=queue;
    }

    @Override
    public void run() {
        while (true) {
            synchronized (queue) {
                while (queue.size() <= 0) {
                    System.out.println("队列空了");
                    try {
                        queue.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                Message msg = queue.poll();
                System.out.println("code: " + msg.getCode() + " msg: " + msg.getMsg());
                queue.notifyAll();
            }
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        Queue<Message> queue =new LinkedList<>();

        Thread producer =new Producer(queue,10);
        Thread consumer =new Consumer(queue);

        producer.start();
        consumer.start();
    }
}
```

### 二叉树

满二叉树满足如下性质：

1. 深度为k的满二叉树节点总数为2^k-1，奇数个
2. 第i层的节点个数为2^(i-1)

完全二叉树：

1. n个节点的完全二叉树的深度为int_down(logn)+1 (int_down为向下取整)

### Master公式

用来计算分支策略的时间复杂度，问题一般分为三步：分解、解决、合并，主方法的表现形式为

```
T[n]=aT[n/b]+f(n)
```

其中a>=1 and b>1是常量，其表示的意义：n表示问题的规模，a表示递归的次数也就是生成的子问题数，b表示每次递归是原来的1/b的规模，f(n)表示分解和合并所要花费的时间之和。

解法：
①当d<logb a时，时间复杂度为O(n^(logb a))
②当d=logb a时，时间复杂度为O((n^d)*logn)
③当d>logb a时，时间复杂度为O(n^d)

### 排序算法

参考：<https://github.com/francistao/LearningNotes/blob/master/Part3/Algorithm/Sort/%E9%9D%A2%E8%AF%95%E4%B8%AD%E7%9A%84%2010%20%E5%A4%A7%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E6%80%BB%E7%BB%93.md>

稳定排序和不稳定排序：<https://www.cnblogs.com/codingmylife/archive/2012/10/21/2732980.html>

#### 快排

快排的时间复杂度平均为O(nlogn)

最坏的情况是每次取到数组中最小/最大的元素，这种情况等同冒泡排序，时间复杂度 n*(n-1) =n^2-n 即O(n)。

最优的情况是每次取到的元素都刚好平分整个数组。此时可根据master公式

**T[n] = aT[n/b] + f(n)**   a=2，b=2 -> **T[n] = 2T[n/2] + f(n)** 

根据公式迭代推导可得 快排的最优时间复杂度 **T[n] = 2^(logn) T[1] + nlogn  =  n T[1] + nlogn  =  n + nlogn** 

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

#### 堆排序

常考题。leetcode 215 题解就是堆排序稍微变动一下。

```java
public void heapSort(int[] nums){
        int n =nums.length;
        buildHeap(nums,n);
        for(int i=n-1;i>=0;i--){
            swap(nums,0,i);
            heapfiy(nums,i,0);
        }
    }

public void buildHeap(int[] nums, int n){
    for(int i=n/2-1;i>=0;i--){
        heapfiy(nums,n,i);
    }
}

//堆化
public void heapfiy(int[] nums ,int n ,int parent){
    if(parent>=n) return;
    int l =2*parent+1;int r =2*parent+2;
    int max=parent;
    if(l<n&&nums[l]>nums[max]) max=l;
    if(r<n&&nums[r]>nums[max]) max=r;
    if(max!=parent){
        swap(nums,max,parent);
        heapfiy(nums,n,max);
    }
}
public void swap(int[] nums,int i, int j){
    int tmp=nums[j];
    nums[j]=nums[i];
    nums[i]=tmp;
}
```







### leetcode

#### [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

i从尾开始好理解一些

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s==null||s.length()==0) return s;
        char[] chs =s.toCharArray();
        int n=s.length();
        boolean[][] dp= new boolean[n][n];
        int start =0;
        int end =0;
        for(int i=n-1;i>=0;i--){
            for(int j=i;j<n;j++){
                if(chs[i]==chs[j]&&(j-i<3||dp[i+1][j-1])){
                    dp[i][j]=true;
                    if(j-i>end-start){
                        start=i;
                        end=j;
                    }
                }else{
                    dp[i][j]=false;
                }
            }
        }
        return s.substring(start,end+1);
    }
}
```



```java
class Solution {
    public String longestPalindrome(String s) {
        if(s==null||s.length()==0) return s;
        int n =s.length();
        char[] a =s.toCharArray();
        boolean[][] dp =new boolean[n][n];
        int len=1;//回文串长度
        int start=0;//回文串起始位置
        for(int j=1;j<n;j++){
            for(int i=0;i<j;i++){
                if(a[i]==a[j]&&(j-i<3||dp[i+1][j-1])){
                    dp[i][j]=true;
                    if(j-i+1>len){
                        len=j-i+1;
                        start=i;
                    }
                }

            }
        }
        return s.substring(start,start+len);
    }
}
```

### 

#### [11. 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

双指针法，一前一后向内移动，每次移动高度小的指针。

```java
class Solution {
    public int maxArea(int[] height) {
        int l =0,r=height.length-1;
        int s =0;
        while(l<r){
            s = Math.max(s,Math.min(height[l],height[r])*(r-l));
            if(height[l]>height[r]) {
                r--;
            }else{
                l++;
            }
        }
        return s;
    }
}
```

#### [15. 三数之和](https://leetcode-cn.com/problems/3sum/)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n =nums.length;
        Arrays.sort(nums);
        List<List<Integer>> list =new ArrayList<>();
        for(int first=0;first<n;first++){
            if(first>0&&nums[first]==nums[first-1]) continue;
            int third =n-1;
            int target =-nums[first];

            for(int second =first+1;second<third;second++){
                if(second>first+1&&nums[second]==nums[second-1]) continue;

                while(third>second&&nums[third]+nums[second]>target){
                    third--;
                }
                if (second == third) {
                    break;
                }
                if(nums[second]+nums[third]==target){
                    ArrayList<Integer> itList =new ArrayList<>();
                    itList.add(nums[first]);
                    itList.add(nums[second]);
                    itList.add(nums[third]);
                    list.add(itList);
                }

            }

        }
        return list;
    }
}
```



#### [25. K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dumb =new ListNode(0);
        dumb.next=head;

        ListNode pre =dumb;
        ListNode end =dumb;//子链表的尾
        while(end!=null){
            for(int i=0;i<k;i++){
                end=end.next;
                if(end==null) return dumb.next;
            }
            ListNode start =pre.next;//子链表的头
            ListNode nex=end.next;//记录链表尾部的下一个节点
            end.next=null;//子链表尾部置空，方便下一行的反转
            pre.next =reverseListNode(start);//反转子链表 pre.next =子链表的新头节点
            start.next=nex;//原来start是子链表头，现在是子链表的尾

            //移动pre和end
            pre=start;
            end=pre;
        }
        return dumb.next;

    }
    public ListNode reverseListNode(ListNode head) {
        ListNode cur =null;
        ListNode h=head; 
        ListNode tmp;
        while(h!=null){
            tmp = h.next;
            h.next=cur;
            
            cur =h;
            h=tmp;
        }
        //此时 cur是头节点 
        return cur;
    }
}
```



#### [31. 下一个排列](https://leetcode-cn.com/problems/next-permutation/)

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int n =nums.length-1;
        //从后往前找到第一个不满足降序排列的元素
        int i=n-1;
        while(i>=0&&nums[i]>=nums[i+1]){
            i--;
        }
        if(i<0){
            reverseArray(nums);
            return;
        }
        int j=n;
        //从i+1往后找到大于nums[i]的最小的数
        while(j>=0&&nums[j]<=nums[i]){
            j--;
        }
        swap(nums,i,j);
        Arrays.sort(nums,i+1,n+1);
        
    }
    public void reverseArray(int[] nums){
        int i =0;
        int j=nums.length-1;
        while(i<j){
            swap(nums,i,j);
            i++;j--;
        }
    }
    public void swap(int[] nums,int i, int j){
        int tmp=nums[j];
        nums[j]=nums[i];
        nums[i]=tmp;
    }
}
```



#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

看题解，讲得很详细。<https://leetcode-cn.com/problems/search-in-rotated-sorted-array/solution/sou-suo-xuan-zhuan-pai-xu-shu-zu-by-leetcode-solut/>

```java
class Solution {
    public int search(int[] nums, int target) {
        int n=nums.length;
        if(n==0) return -1;
        if(n==1) return nums[0]==target?0:-1;
        int l=0,r=n-1;
        
        //注意r>=l
        while(l<=r){
            int mid = (l+r)/2;
            if(nums[mid]==target) return mid;
            //先找到有序的区间，if条件成立则左边有序
            if(nums[mid]>=nums[0]){
                //target在左边区间的话
                if(nums[0]<=target&&target<nums[mid]){
                    r=mid-1;
                }else{
                    l=mid+1;
                }
                //右边有序
            }else{
                //在区间内
                if(nums[mid]<target&&target<=nums[n-1]){
                    l=mid+1;
                }else{
                    r=mid-1;
                }
            }
        }
        return -1;
    }
}
```



#### [39. 组合总和](https://leetcode-cn.com/problems/combination-sum/)

相比40题，不用检查上一个是否重复，只要做一个<0的剪枝即可。由于可以重复，下次计算的index=i。

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] cand, int target) {

        Arrays.sort(cand);
        return dfs(cand,target,0,new ArrayList<>(),new ArrayList<>());
    }

    List<List<Integer>> dfs(int[] cand , int target,int index, List<Integer> list,List<List<Integer>> rslist){
        if(target==0){
            rslist.add(new ArrayList<>(list));
            return rslist;
        }
        for(int i=index;i<cand.length;i++){
            if(target-cand[i]<0) break;
            list.add(cand[i]);
            dfs(cand,target-cand[i],i,list,rslist);
            list.remove(list.size()-1);
        }
        return rslist;
    }
}
```



#### [40. 组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

46，47排列问题，两种问题的区别是排列需要used记录，每次for从0开始；而组合不要，每次从上一个index+1开始。

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] cand, int target) {
        Arrays.sort(cand);
        return dfs(cand,target,0,new ArrayList<>(),new ArrayList<>());
    }

    List<List<Integer>> dfs(int[] cand,int target ,int index,List<Integer> list,List<List<Integer>> rsList){
        if(target==0){
            rsList.add(new ArrayList<>(list));
            return rsList;
        }
        for(int i=index;i<cand.length;i++){
            if(target-cand[i]<0) break;
            if(i>index&&cand[i]==cand[i-1]) continue;
            list.add(cand[i]);
            dfs(cand,target-cand[i],i+1,list,rsList);
            list.remove(list.size()-1);
        }
        return rsList;
    }
}
```



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

#### [41. 缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        int n=nums.length;
        
        for(int i=0;i<n;i++){
            if(nums[i]<=0){
                nums[i]=n+1;
            }
        }
        for(int i=0;i<n;i++){
            int index =Math.abs(nums[i])-1;
            if(index<n) nums[index]=-Math.abs(nums[index]);
        }
        for(int i=0;i<n;i++){
            if(nums[i]>0){
                return i+1;
            }
        }
        return n+1;
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



#### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

迭代的方法比较好理解，注意细节即可。面试可能要求递归写法，也要掌握。

```java
class Solution {
    public double myPow(double x, int n) {
        boolean flag =false;
        long p = n;//这里有个坑，n可能为-2147483648 直接取反再赋值给n就溢出了。
        if(p<0){
            flag=true;
            p=-p;
        }
        double base =x;
        double res =1.0;
        while(p>0){
            if((p&1)!=0){
                res*=base;
            }
            p>>=1;
            base*=base;
        }
        return flag?(1.0/res):res;
    }
}
```

递归方法

参考<https://leetcode-cn.com/problems/powx-n/solution/powx-n-by-leetcode-solution/>

```java
class Solution {
    public double myPow(double x, int n) {
        
        long N =n;
        return n>0?pow(x,N):1.0/pow(x,-N);
    }

    public double pow(double x,long n){
        if(n==0){
            return 1.0;
        }
        double y =pow(x,n/2);
        return (n&1)==0?y*y:y*y*x;
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

#### [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

和54题做法类似。

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res =new int[n][n];
        if(n==0) return res;
        int left =0;int right = n-1;int bottom =0;int top =n-1;
        int cur =1;
        while(cur<=n*n){
            //向右
            for(int i=left;i<=right;i++){
                res[bottom][i]=cur++;
            }
            //向下
            for(int i=bottom+1;i<=top;i++){
                res[i][right]=cur++;
            }
            if(bottom<top){
                for(int i=right-1;i>=left;i--){
                    res[top][i]=cur++;
                }
            }
            if(right>left){
                for(int i=top-1;i>bottom;i--){
                    res[i][left]=cur++;
                }
            }
            left++;
            bottom++;
            right--;
            top--;
        }
        return res;
    }
}
```



#### 64 最小路径和

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

#### [69. x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

1.二分法  2.牛顿迭代法

```java
class Solution {
    // f(x)=x*x-a
    // f(x) =f(x0)+(x-x0)f'(x)
    //f(x)=0
    //x=-f(x0)/f'(x)+x0
    //x=x0代入
    //x=(-1/2)*(x0-a/x0)+x0 =(1/2)*(x0+a/x0)
    public int mySqrt(int x) {
        long res =x ;
        while(res*res>x){
            res=(res+x/res)>>1;
        }
        return (int)res;
    }
}
```



#### [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

头插法。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dumb = new ListNode(0);
        dumb.next=head;
        ListNode pre =dumb;
        ListNode node =dumb;

        while(m>0){
            pre=node;
            node=node.next;
            n--;
            m--;
        }
        //pre是中间链表表头的前一个节点
        ListNode removed;
        while(n>0){
            removed=node.next;
            node.next=node.next.next；
            
            removed.next =pre.next;
            pre.next=removed;
            n--;
        }
        return dumb.next;
    }
}
```

递归实现，理解起来比较困难，注意理解时不要跳进递归，而是利用明确的定义来实现算法逻辑。

参考详解：<https://leetcode-cn.com/problems/reverse-linked-list-ii/solution/bu-bu-chai-jie-ru-he-di-gui-di-fan-zhuan-lian-biao/>

```java
class Solution {
    //递归的实现
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if(m==1){
            return reverseN(head,n);
 
        }
        head.next =reverseBetween(head.next,m-1,n-1);
        return head;
    }
    ListNode s;
    public ListNode reverseN(ListNode head,int n){
        if(n==1){
            s=head.next;//记录head下一个节点
            return head;
        }
        ListNode last=reverseN(head.next,n-1);
        head.next.next =head;
        head.next =s;
        return last;
    }
}
```



#### [103. 二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

入队的顺序不用变，遍历队列中元素的时候，一层头插list.addFirst()，下一层尾插list.addLast()

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        LinkedList<Integer> list =new LinkedList<>();
        List<List<Integer>> rslist =new ArrayList<>();
        if(root==null) return rslist;
        Queue<TreeNode> queue =new LinkedList<>();
        queue.add(root);
        int cnt =1;
        boolean flag =true;
        while(!queue.isEmpty()){
            TreeNode t = queue.poll();
            if(flag){
                list.addLast(t.val);
            }else{
                list.addFirst(t.val);
            }
            cnt--;
            if(t.left!=null) queue.add(t.left);
            if(t.right!=null) queue.add(t.right);
            
            if(cnt==0){
                cnt =queue.size();
                flag=!flag;
                rslist.add(new LinkedList<>(list));
                list =new LinkedList<>();
            }
        }
        return rslist;
    }
}
```





#### [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

非递归，借助栈。stack先push左子节点，直到为空，此时取出栈顶的第一个节点tmp，再做前面的操作......当栈为空并且tmp为空时退出循环。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        TreeNode r =root;
        List<Integer> list =new ArrayList<>();
        if(root==null) return list;
        Stack<TreeNode> stack =new Stack<>();
        // stack.push(root);
        while(!stack.isEmpty()||r!=null){
            if(r!=null){
                stack.push(r);
                r=r.left;
            }
            else{
                TreeNode n =stack.pop();
                list.add(n.val);
                r =n.right;
            }
        }
        return list;
    }
}
```

#### [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

递归和迭代，迭代借助队列比较简单，这里只贴出递归的写法。

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list =new ArrayList<>();
        if(root==null) return list;
        dfs(root,1,list);
        return list;
    }

    void dfs(TreeNode root ,int index ,List<List<Integer>> list){
        if(list.size()<index){
            list.add(new ArrayList<>());
        }
        list.get(index-1).add(root.val);
        if(root.left!=null){
            dfs(root.left,index+1,list);
        }
        if(root.right!=null){
            dfs(root.right,index+1,list);
        }
    }
}
```



#### [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

这个题跟最大深度差不多，但是有个小坑。

这道题的关键是搞清楚递归结束条件

叶子节点的定义是左孩子和右孩子都为 null 时叫做叶子节点
当 root 节点左右孩子都为空时，返回 1
当 root 节点左右孩子有一个为空时，返回不为空的孩子节点的深度
当 root 节点左右孩子都不为空时，返回左右孩子较小深度的节点值

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int minDepth(TreeNode root) {
        if(root==null) return 0;
        int left =minDepth(root.left);
        int right = minDepth(root.right);
        return root.left==null||root.right==null?left+right+1:Math.min(left,right)+1;
    }
}
```

非递归的方式如下。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //非递归
    public int minDepth(TreeNode root) {
        if(root==null) return 0;
        Queue<TreeNode> queue =new LinkedList<>();
        queue.add(root);
        int depth =0;
        int size =1;
        while(!queue.isEmpty()){
            TreeNode t =queue.poll();
            size--;
            if(t.left==null&&t.right==null){
                return depth+1;
            }
            if(t.left!=null) queue.add(t.left);
            if(t.right!=null) queue.add(t.right);
            if(size==0){
                depth++;
                size=queue.size();
            }
        }
        return 0;
    }
```

#### [118. 杨辉三角](https://leetcode-cn.com/problems/pascals-triangle/)

杨辉三角的生成，找规律题。

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res =new ArrayList<>();
        List<Integer> sub =new ArrayList<>();
        for(int i=0;i<numRows;i++){
            for(int j=0;j<=i;j++){
                if(j==0||j==i){
                    sub.add(1);
                }else{
                    sub.add(res.get(i-1).get(j-1)+res.get(i-1).get(j));
                }
            }
            res.add(new ArrayList<>(sub));
            sub=new ArrayList<>();
        }
        return res;
    }
}
```

#### [119. 杨辉三角 II](https://leetcode-cn.com/problems/pascals-triangle-ii/)

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> list =new ArrayList<>();
        for(int i=0;i<=rowIndex;i++){
            list.add(1);
            //由于循环中计算list中j的值用到了list的j-1的值，
            //所以应该从后往前遍历
            //第一个元素和最后一个元素固定为1不动，修改其他位置元素
            for(int j=list.size()-2;j>0;j--){
                list.set(j,list.get(j)+list.get(j-1));
            }
        }
        return list;
    }
}
```

#### [123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

这道题很多题解都是复杂的动态规划（理解困难），实际上遍历两遍数组就可以，本质上是把prices数组拆分成两个，第一次交易再前半部分，第二次交易在后半部分。

参考：<https://www.bilibili.com/video/BV1ED4y1Q7AP>

```java
class Solution {
    public int maxProfit(int[] prices) {
        //由于只能买卖两次，因此两次遍历prices数组
        //一次从头到尾Ldp，一次从尾到头Rdp
        //找到Ldp[i]+Rdp[i]的最大值
        int n =prices.length;
        if(prices==null||n<2){return 0;}
        //从左往右
        int[] Ldp =new int[n];
        int min =prices[0];Ldp[0]=0;
        for(int i=1;i<n;i++){
            if(min>prices[i]){
                min=prices[i];
            }
            Ldp[i]=Math.max(prices[i]-min,Ldp[i-1]);
        }

        int[] Rdp =new int[n];
        int max =prices[n-1];
        Rdp[n-1]=0;
        for(int j=n-2;j>=0;j--){
            if(prices[j]>max){
                max=prices[j];
            }
            Rdp[j]=Math.max(max-prices[j],Rdp[j+1]);
        }
        int res = 0;
        for(int k=0;k<n;k++){
            res =Math.max(res,Rdp[k]+Ldp[k]);
        }
        return res;
    }
}
```



#### [143. 重排链表](https://leetcode-cn.com/problems/reorder-list/)

先找到中间节点，然后反转后半部分链表，然后合并反转后的后半部分和前半部分

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public void reorderList(ListNode head) {
        if(head==null) return;
        ListNode before =head;
        ListNode midNode =getMidNode(head);//拿到中间节点

        //反转后半段的链表
        ListNode behind =midNode.next;
        midNode.next=null;
        behind = reverse(behind);
        // midNode.next=null;
        merge(before,behind);
    }
    void merge(ListNode before,ListNode behind){
        while(behind!=null){
            ListNode nex1 =before.next;
            before.next =behind;
            ListNode nex2 =behind.next;
            behind.next=nex1;
            behind=nex2;
            before=nex1;
        }
    }
    ListNode reverse(ListNode node){
        ListNode tmp =node;
        ListNode p1 =node;
        ListNode p2 =null;
        while(tmp!=null){
            p1=tmp.next;
            tmp.next=p2;
            p2=tmp;
            tmp=p1;
        }
        return p2;
    }
    ListNode getMidNode(ListNode node){
        if(node ==null) return null;
        ListNode slow =node;
        ListNode fast =node;
        while(fast!=null&&fast.next!=null){
            slow=slow.next;
            fast=fast.next.next;
        }
        return slow;
    }
}
```



#### [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

递归的很简单就不用说了，主要看非递归的。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //非递归
    public List<Integer> preorderTraversal(TreeNode root) {
        // TreeNode r =root;
        Stack<TreeNode> stack =new Stack<>();
        List<Integer> list =new ArrayList<>();
        if(root==null) return list;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode n =stack.pop();
            list.add(n.val);
            if(n.right!=null){
                stack.push(n.right);
            }
            if(n.left!=null){
                stack.push(n.left);
            }
        }
        return list;
    }
}
```

#### [146. LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

面试场考题目。其中链表可以使用LinkedList，也可以自己实现一个双向链表。使用LinkedList精简版代码如下。

```java
class LRUCache {
    HashMap<Integer,Node> map =new HashMap<>();
    LinkedList<Node> list =new LinkedList<>();
    int capacity;
    public LRUCache(int capacity) {
        this.capacity=capacity;
    }
    
    public int get(int key) {
        if(map.containsKey(key)){
            Node n =map.get(key);
            //移动节点到链表头部
            list.remove(n);
            list.addFirst(n);
            return n.value;
        }
        return -1;
    }
    
    public void put(int key, int value) {
        //检查是否已经存在key
        if(map.containsKey(key)){
            //存在 移动到头部
            Node n =map.get(key);
            n.value=value;
            list.remove(n);
            list.addFirst(n);
            map.put(key,n);
        }else {
            if(map.size()==capacity){  //不存在 检查容量是否够
                //丢掉最后一个节点
                Node r =list.removeLast();
                map.remove(r.key);
            }
            Node n =new Node(key,value);
            list.addFirst(n);
            map.put(key,n);
        }
    }
}

class Node{
    int key;
    int value;
    public Node(int key, int value){
        this.key=key;
        this.value=value;
    }
    
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```



#### [128. 最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

每次更新连续数组的边界值为当前连续数组的长度，。

map.put(nums[i],0) 只是表明该数已经被访问了，这里的value可以是任何值

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if(nums.length==0) return 0;
        Map<Integer,Integer> map =new HashMap<>();
        int max =1;
        for(int i=0;i<nums.length;i++){
            if(!map.containsKey(nums[i])){
                int left =map.getOrDefault(nums[i]-1,0);
                int right =map.getOrDefault(nums[i]+1,0);
                int cur =left+right+1;
                if(cur>max){
                    max= cur;
                }
                map.put(nums[i],0);
                map.put(nums[i]-left,cur);
                map.put(nums[i]+right,cur);
            }
        }
        return max;
    }
}
```



#### [129. 求根到叶子节点数字之和](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)

递归，空返回0；左树空&&右树空返回n；有一个不为空继续往下加和。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int sumNumbers(TreeNode root) {
        return sumNumbersHelper(root,0);
    }
    public int  sumNumbersHelper(TreeNode root,int val){
        if(root==null) {
            return 0;
        }
        val = 10*val+root.val;
        if(root.left==null&&root.right==null){
            return val;
        }
        int left = sumNumbersHelper(root.left,val);
        int right = sumNumbersHelper(root.right,val);
        return left+right;
    }
}
```



#### [199. 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //深搜递归
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list =new ArrayList<>();
        dfs(root,list,0);
        return list;
    }
    public void dfs(TreeNode root,List<Integer> list,int depth){
        if(root==null) return;
        if(depth==list.size()){
            list.add(root.val);
        }
        depth++;
        dfs(root.right,list,depth);
        dfs(root.left,list,depth);
    }

    //广搜
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list =new ArrayList<>();
        if(root==null) return list;
        Queue<TreeNode> queue =new LinkedList<>();
        queue.add(root);
        int cnt=1;
        while(!queue.isEmpty()){
            TreeNode t =queue.poll();
            if(t.left!=null) queue.add(t.left);
            if(t.right!=null) queue.add(t.right);
            cnt--;
            if(cnt ==0){
                list.add(t.val);
                cnt= queue.size();
            }
        }
        return list;

    }
}
```



#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

堆排序求解！

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        //堆排序
        heapSort(nums,k);
        return nums[nums.length-k]; 
    }
    public void heapSort(int[] nums,int k){
        int n =nums.length;
        buildHeap(nums,n);
        for(int i=n-1;i>=n-k;i--){
            swap(nums,0,i);
            heapfiy(nums,i,0);
        }
    }

    public void buildHeap(int[] nums, int n){
        for(int i=n/2-1;i>=0;i--){
            heapfiy(nums,n,i);
        }
    }

    //堆化
    public void heapfiy(int[] nums ,int n ,int parent){
        if(parent>=n) return;
        int l =2*parent+1;int r =2*parent+2;
        int max=parent;
        if(l<n&&nums[l]>nums[max]) max=l;
        if(r<n&&nums[r]>nums[max]) max=r;
        if(max!=parent){
            swap(nums,max,parent);
            heapfiy(nums,n,max);
        }
    }
    public void swap(int[] nums,int i, int j){
        int tmp=nums[j];
        nums[j]=nums[i];
        nums[i]=tmp;
    }

}
```



#### [208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)

这道题应该将节点抽象成单独类，容易理解和编写代码。暂时放上能通过的粗糙版代码。如果前缀树存储中文的话，就不能使用数组了，而应该用Map。

```java
class Trie {
    public Trie[] trie;
    public boolean isEnd;
    private final int R=26;
    /** Initialize your data structure here. */
    public Trie() {
        trie=new Trie[R];
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        char[] chars = word.toCharArray();
        Trie t =this;
        for(int i=0;i<chars.length;i++){
            Trie[] tnext=t.trie;
            if(tnext[chars[i]-'a']==null){
                tnext[chars[i]-'a'] =new Trie();
            }
            t=tnext[chars[i]-'a'];
        }
        t.isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        char[] chars = word.toCharArray();
        Trie t =this;
        for(int i=0;i<chars.length;i++){
            Trie[] tnext=t.trie;
            // if(i==chars.length-1&&tnext[chars[i]-'a']!=null&&t.isEnd) return true;
            if(tnext[chars[i]-'a']==null) {
                return false;
            }else{
                t=tnext[chars[i]-'a'];
            } 
        }
        return t.isEnd;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        char[] chars = prefix.toCharArray();
        Trie t =this;
        for(int i=0;i<chars.length;i++){
            Trie[] tnext=t.trie;
            if(tnext[chars[i]-'a']==null) {
                return false;
            }else{
                t=tnext[chars[i]-'a'];
            } 
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

重写代码如下，自定义node类

```java
class Trie {
    private TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root =new TrieNode();
    }
    /** Inserts a word into the trie. */
    public void insert(String word) {
        char[] chars =word.toCharArray();
        TrieNode n =root;
        for(int i=0;i<chars.length;i++){
            char ch =chars[i];
            if(!n.contains(ch)){
                n.put(ch);
            }
            n=n.get(ch);
        }
        n.setEnd();
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        char[] chars =word.toCharArray();
        TrieNode n =root;
        for(int i=0;i<chars.length;i++){
            char ch =chars[i];
            if(!n.contains(ch)) return false;
            else{
                n=n.get(ch);
            }
        }
        return n.isEnd();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        char[] chars =prefix.toCharArray();
        TrieNode n =root;
        for(int i=0;i<chars.length;i++){
            char ch =chars[i];
            if(!n.contains(ch)) return false;
            else{
                n=n.get(ch);
            }
        }
        return true;
    }
}

class TrieNode{
    private TrieNode[] next;
    private boolean isEnd;
    private final int R =26;
    public TrieNode(){
        next =new TrieNode[R];
    }
    public TrieNode get(char ch){
        return next[ch-'a'];
    }
    public void put(char ch){
        next[ch-'a'] =new TrieNode();
    }
    public boolean contains(char ch){
        return next[ch-'a']!=null;
    }
    public boolean isEnd(){
        return isEnd;
    }
    public void setEnd(){
        isEnd=true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```



#### [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

最优解：快慢指针，快指针每次走两个节点，慢指针每次一个节点，每次走的时候，将节点next指向反转。直到退出循环，如果是回文链表，此时前半部分和后半部分是一致的。

 if(fast!=null) slow = slow.next; 这段是当链表节点为奇数个时，跳过中间那个节点。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head==null||head.next==null) return true;
        ListNode slow =head;
        ListNode fast =head;
        ListNode pre = null;
        ListNode cur = head;
        //遍历的同时,进行反转
        while(fast!=null&&fast.next!=null){
            cur =slow;
            slow =slow.next;
            fast =fast.next.next;
            cur.next=pre;
            pre =cur;
        }
        //cur是前半部分反转后的头节点   
        //此时的slow是后半部分的头节点
        //如果是奇数个节点的话 现在fast!=null,slow还需要往下走一步,因为中间那个节点不用比较需要跳过。
        //偶数节点则不用
        if(fast!=null) slow = slow.next;
        while(slow!=null){
            if(slow.val!=cur.val) return false;
            slow =slow.next;
            cur= cur.next;
        }
        return true;
    }
}
```

#### 252.会议室

按开始时间进行排序，判断数组中当前元素开始时间是否小于前一个结束时间，是则cnt++，否则继续循环。

#### 253.会议室2

<https://blog.csdn.net/qinian_ztc/article/details/105257168>

#### [283. 移动零](https://leetcode-cn.com/problems/move-zeroes/)

双指针，各自遍历一次。

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int j =0 ;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=0){
                nums[j++]=nums[i];
            }
        }
        for(;j<nums.length;j++){
            nums[j]=0;
        }
    }
}
```

或者双指针，一次遍历

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int j =0 ;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=0){
                int tmp =nums[i];
                nums[i]=nums[j];
                nums[j++]=tmp;
            }
        }
    }
}
```



#### [309. 最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

三种状态的转换，动态规划。

参考：<https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/solution/yi-tu-miao-dong-jie-fa-by-zi-gei-zi-zu/>

```java
class Solution {
    public int maxProfit(int[] prices) {
        int n =prices.length;
        if(n<2) return 0;
        int[][] dp =new int[n][3];
        //0-持有   1-不持有 冷冻期不可买  2-不持有 可买
        dp[0][0]=-prices[0];
        for(int i=1;i<n;i++){
            dp[i][0] =Math.max(dp[i-1][0],dp[i-1][2]-prices[i]);
            dp[i][1] =dp[i-1][0]+prices[i];
            dp[i][2] =Math.max(dp[i-1][1],dp[i-1][2]);
        }
        return Math.max(dp[n-1][1],dp[n-1][2]);
    }
}
```



#### [322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

自顶向下---dfs，自底向上--动态规划。dp[0]=0很巧妙，这样当i=coins[j]时，dp[i-coin]+1=1表示使用coin一次。

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp =new int[amount+1];
        Arrays.fill(dp,amount+1);
        dp[0]=0;
        
        for(int i=1;i<=amount;i++){
            for(int j=0;j<coins.length;j++){
                if(coins[j]<=i){
                    dp[i]=Math.min(dp[i],dp[i-coins[j]]+1);
                }
            }
        }
        return dp[amount]>amount?-1:dp[amount];
    }
}
```



#### [337. 打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)

暴力解法

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int rob(TreeNode root) {
        if(root==null) return 0;
        int val =root.val;
        if(root.left!=null){
            val+=(rob(root.left.left)+rob(root.left.right));
        }
        if(root.right!=null){
            val+=(rob(root.right.left)+rob(root.right.right));
        }
        return Math.max(val,rob(root.left)+rob(root.right));
    }
}
```

#### [410. 分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)

理解起来困难，其实代码不复杂。

```java
class Solution {
    public int splitArray(int[] nums, int m) {
        int max =0;
        int sum =0;
        for(int num:nums){
            max =Math.max(max,num);
            sum+=num;
        }
        //子数组各自和的最大值取值范围在[max,sum]之间
        //二分法找 满足分区个数为m时的maxSubArrayVal
        int left = max;
        int right =sum;
        while(left<right){
            int mid =left + (right-left)/2;
            int splits = getPartiton(nums,mid);
            if(splits>m){ //分区太多
                left=mid+1;
            }else{
                right=mid;
            }
        }
        return left;
    }
    public int getPartiton(int[] nums,int mid){
        int splits =1;
        int curSum=0;
        for(int i=0;i<nums.length;i++){
            if(curSum+nums[i]>mid){
                curSum=0;
                splits++;
            }
            curSum+=nums[i];
        }
        return splits;
    }
}
```

#### [424. 替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int[] map =new int[26];
        char[] chs =s.toCharArray();
        int left=0,right=0;
        int result=0;
        int maxCharCount = 0;
        while(right<s.length()){
            map[chs[right]-'A']++;
            maxCharCount=Math.max(maxCharCount,map[chs[right]-'A']);
            if(right-left+1-maxCharCount>k){
                map[chs[left]-'A']--;
                left++;
            }
            result=Math.max(result,right-left+1);
            right++;
        }
        return result;
    }
}
```



#### [470. 用 Rand7() 实现 Rand10()](https://leetcode-cn.com/problems/implement-rand10-using-rand7/)

拒绝采样，关键是知晓如下规律

已知 rand_N() 可以等概率的生成[1, N]范围的随机数
那么：
(rand_X() - 1) × Y + rand_Y() ==> 可以等概率的生成[1, X * Y]范围的随机数
即实现了 rand_XY()

作者：kkbill
链接：https://leetcode-cn.com/problems/implement-rand10-using-rand7/solution/cong-zui-ji-chu-de-jiang-qi-ru-he-zuo-dao-jun-yun-/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



#### [516. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

与第5题对应。dp公式好理解，遍历的顺序难理解，理解dp是一个很难的过程。这里的dp从底下开始网上遍历。

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int n =s.length();
        if(n==0) return 0;
        char[] a =s.toCharArray();
        int[][] dp =new int[n][n];
        for(int i=n-1;i>=0;i--){
            dp[i][i]=1;
            for(int j=i+1;j<n;j++){
                if(a[i]==a[j]){
                    dp[i][j]=dp[i+1][j-1]+2;
                }
                else{
                    dp[i][j]=Math.max(dp[i+1][j],dp[i][j-1]);
                }
            }
        }
        return dp[0][n-1];
    }
}
```

#### [540. 有序数组中的单一元素](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/)

log(n)时间复杂度需要二分法。解题关键是找到mid，看哪边长度是奇数，则目标数肯定在那边，否则在另一边。

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int l =0,r =nums.length-1;
        while(l<r){
            int mid =(l+r)/2;
            if(nums[mid]==nums[mid+1]){
                if((mid-l)%2==0){//左边为偶数个数 搜索右边
                    l=mid+2;
                }else{
                    r=mid-1;
                }
            }else if(nums[mid]==nums[mid-1]){
                if((mid-l)%2==0){//左边为奇数个数 搜索左边
                    r=mid-2;
                }else{
                    l=mid+1;
                }
            }else{
                return nums[mid];
            }
        }
        return nums[l];
    }
}
```

#### [543. 二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int ans=1;
    public int diameterOfBinaryTree(TreeNode root) {
        if(root==null) return 0;
        helper(root);
        return ans-1;
    }
    public int helper(TreeNode root){
        if(root==null) return 0;
        int left =helper(root.left);
        int right =helper(root.right);
        ans = Math.max(ans,left+right+1);
        return Math.max(left,right)+1;
    }
}
```

#### [679. 24 点游戏](https://leetcode-cn.com/problems/24-game/)

```java
class Solution {
    static final int TARGET = 24;
    static final double EPSILON = 1e-6;
    static final int ADD = 0, MULTIPLY = 1, SUBTRACT = 2, DIVIDE = 3;
    public boolean judgePoint24(int[] nums) {
        List<Double> list =new ArrayList<>();
        for(int num:nums){
            list.add((double)num);
        }
        return solve(list);

    }

    public boolean solve(List<Double> list){
        int size =list.size();
        if(list.size()==0) return false;
        if(list.size()==1) return Math.abs(list.get(0)-TARGET)<EPSILON;
        for(int i=0;i<size;i++){
            for(int j=0;j<size;j++){
                
                if(i!=j){
                    List<Double> list2 =new ArrayList<>();
                    for(int k=0;k<size;k++){
                        if(k!=i&&k!=j) list2.add(list.get(k));
                    }
                    for(int k=0;k<4;k++){
                        if(k<2&&i>j) {continue;}
                        if(k==ADD){//加
                            list2.add(list.get(i)+list.get(j));
                        }
                        else if(k==MULTIPLY){//乘
                            list2.add(list.get(i)*list.get(j));
                        }
                        else if(k==SUBTRACT){//减
                            list2.add(list.get(i)-list.get(j));
                        }
                        else if(k==DIVIDE){//除
                            if(Math.abs(list.get(j))<EPSILON) continue;
                            else list2.add(list.get(i)/list.get(j));
                        }
                        if(solve(list2)){
                            return true;
                        }
                        list2.remove(list2.size()-1);
                    }
                }
            }
        }
        return false;
    }
}
```



#### [885. 螺旋矩阵 III](https://leetcode-cn.com/problems/spiral-matrix-iii/)

```java
class Solution {
    public int[][] spiralMatrixIII(int R, int C, int r0, int c0) {
        int[][] steps =new int[][]{
            {0,1},{1,0},{0,-1},{-1,0}
            };
        int n =0;//方向 0-向右 1-向下 2-向左 3-向上
        int m =0;//当次应走的步数
        int[][] res =new int[R*C][2];
        res[0][0]=r0;
        res[0][1]=c0;
        int index = 1;
        while(index<R*C){
            for(int i=0;i<=m;i++){
                r0+=steps[n][0];
                c0+=steps[n][1];
                if(r0>=0&&r0<R&&c0>=0&&c0<C){
                    res[index][0]=r0;
                    res[index][1]=c0;
                    index++;
                }
                if(index==R*C) return res;
            }
            //这两行是算法的关键之处
            m+=(n%2);//每两次的step相等，即n增加2对应m增加1
            n=(n+1)%4;// n=0 ->n=1 ->n=2->n=3 ->n=0.....方向的循环变化
        }
        return res;
    }
}
```



#### [919. 完全二叉树插入器](https://leetcode-cn.com/problems/complete-binary-tree-inserter/)

在初始化的时候，保存根节点，通过queue和deque遍历节点，所有叶子节点存储到deque中。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class CBTInserter {
    TreeNode root;
    Deque<TreeNode> deque;
    public CBTInserter(TreeNode root) {
        this.root =root;
        Queue<TreeNode> queue = new LinkedList<>();
        deque = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            TreeNode t =queue.poll();
            if(t.left==null||t.right==null) deque.addLast(t);//收集叶子节点
            if(t.left!=null) queue.add(t.left);
            if(t.right!=null) queue.add(t.right);
        }
    }
    
    public int insert(int v) {
        TreeNode t =deque.peekFirst();
        TreeNode n =new TreeNode(v);
        deque.addLast(n);
        if(t.left==null){
            t.left =n;
        }
        else{
            t.right=n;
            deque.pollFirst();
        }
        return t.val;
    }
    
    public TreeNode get_root() {
        return root;
    }
}

/**
 * Your CBTInserter object will be instantiated and called as such:
 * CBTInserter obj = new CBTInserter(root);
 * int param_1 = obj.insert(v);
 * TreeNode param_2 = obj.get_root();
 */
```

#### [1226. 哲学家进餐](https://leetcode-cn.com/problems/the-dining-philosophers/)

这个题考察的是如何避免死锁。

死锁的四个必要条件：

1.互斥。同一时间资源只能被一个进程使用。

2.请求和保持。进程至少保持了一个资源，但又提出新的资源请求，而该资源被别的线程占用，此时请求的线程被阻塞，但对自己获得的资源保持不变。

3.循环等待。多个进程之间形成了首尾相接循环等待的资源关系。

4.不可剥夺。资源只能被获得该资源的进程主动释放，不可被强行剥夺。

#### [1312. 让字符串成为回文串的最少插入次数](https://leetcode-cn.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/)

新瓶装旧酒，本质上就是最长回文子序列516题。

```java
class Solution {
    //求最长的回文子序列len，用n-len 即可得到最少插入次数
    public int minInsertions(String s) {
        char[] chs =s.toCharArray();
        int n =s.length();
        int[][] dp =new int[n][n];
        for(int i=n-1;i>=0;i--){
            dp[i][i]=1;
            for(int j=i+1;j<n;j++){
                if(chs[i]==chs[j]){
                    dp[i][j]=dp[i+1][j-1]+2;
                }else{
                    dp[i][j]=Math.max(dp[i+1][j],dp[i][j-1]);
                }
            }
        }
        return n-dp[0][n-1];
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

#### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)



#### 

滑动窗口，空间复杂度O(1)，时间复杂度O(n2)

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s==null||s.length()==0) return 0;
        //滑动窗口
        int max =1;
        int i=0;
        for(int j=0;j<s.length();j++){
            for(int k=i;k<j;k++){
                if(s.charAt(k)==s.charAt(j)){
                    //移动左指针
                    i=k+1;
                    break;
                }
            }
            max =Math.max(max,j-i+1);
        }
        return max;
    }
}
```

滑动窗口+map，空间O(n)，时间O(n)

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s==null||s.length()==0) return 0;
        //滑动窗口
        int max =1;
        int i=0;
        HashMap<Character,Integer> map =new HashMap<>();
        for(int j=0;j<s.length();j++){
            if(map.containsKey(s.charAt(j))){
                i=Math.max(map.get(s.charAt(j))+1,i);
            }
            max =Math.max(max,j-i+1);
            map.put(s.charAt(j),j);
        }
        return max;
    }
}
```

[剑指 Offer 51. 数组中的逆序对](#Offer51)



#### [剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

```java
class Solution {
    public int strToInt(String str) {
        str =str.trim().strip();
        if(str==null||str.length()==0) return 0;
        boolean flag=true;
        int bd =Integer.MAX_VALUE/10;
        // int k=Integer.MAX_VALUE%10;

        int sum=0;
        int i=1;//移动i
        if(str.charAt(0)=='-') {
            flag=false;//负数
        }
        else if(str.charAt(0)!='+') i=0;

        for(int k=i;k<str.length();k++){
            char c =str.charAt(k);
            if(c<'0'||c>'9') break;
            if(sum>bd||sum==bd&&str.charAt(k)>'7') return flag?Integer.MAX_VALUE:Integer.MIN_VALUE; 
            sum=10*sum+(c-'0');
        }
        return flag?sum:-sum;
    }
}
```



#### [剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode l =p.val>q.val?q:p;
        TreeNode r =p.val>q.val?p:q;
        TreeNode t= root;
        while(t!=null){
            if(t.val>r.val){
                t=t.left;
            }else if(t.val<l.val){
                t=t.right;
            }else{
                return t;
            }
        }
        return null;
    }
}
```



#### [剑指 Offer 68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root==null||root==q||root==p) return root;
        TreeNode l =lowestCommonAncestor(root.left,p,q);
        TreeNode r =lowestCommonAncestor(root.right,p,q);
        if(l==null) return r;
        if(r==null) return l;
        return root;
    }
}
```



## 设计模式

六大原则

单一职责原则：一个类只负责一个功能领域的相应职责。

开闭原则：对拓展开发，对修改关闭。



## Java基础

### 注解

java的元注解一共有四个：

1. @Document
2. @Target
3. @Retention
4. @Inherited



### 深拷贝和浅拷贝

定义如下：

浅拷贝（shallowCopy）只是增加了一个指针指向已存在的内存地址，

深拷贝（deepCopy）是增加了一个指针并且申请了一个新的内存，使这个增加的指针指向这个新的内存，

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


### 集合

#### HashMap（没写完）

数组+链表实现的，链表的出现是为了解决hash冲突。HashMap初始化的时候，Entry数组不会实例化，在第一次进行put操作的时候初始化数组。

默认大小size是16，loadFactor默认0.75，threshold是前面两个乘积，当Map中的元素个数超过threshold时，会发生扩容。



put操作的时候，对存储的键值对的key获取hashCode，再进行扰动计算，然后hash&(n-1)得到元素在数组中应该存储的位置，然后从这个位置顺着链表往下对每个元素进行比较（先==再equal）


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

### 单例模式

#### 双检锁

```java
/**
 * 双检锁
 */
public class Singleton1 {
    private volatile static Singleton1 instance ;

    private Singleton1(){}

    public static Singleton1 getInstance(){
        //判断单例对象是否为空，避免不必要的锁获取
        if(instance==null){
            //锁类对象，防止多个线程实例化instance
            synchronized (Singleton1.class){
                //判断单例对象是否为空，避免其他线程在此之前获取到锁，已经进行了实例化
                if(instance==null){
                    instance =new Singleton1();//instance使用volatile修饰，防止指令重排，防止出现线程不安全情况。
                }
            }
        }
        return instance;
    }
}

```

#### 静态内部类

> 注：外部类可以访问到静态内部类的private成员。如果外部类和内部类要访问对方的private/protected成员时，javac编译会生成合适的"access method"----access$xxx形式的方法提供合适的可访问性（通过javap -c反编译字节码可以看到该方法）。

```java
/**
 * 静态内部类
 */
public class Singleton2 {
//    private static Singleton2 instance;

    private Singleton2(){}

    private static class innerClass{
        private static Singleton2 instance =new Singleton2();
    }
    public static Singleton2 getInstance(){
        return innerClass.instance;
    }

}

```



## JVM

### 排查线上问题步骤？



### 锁

#### Synchronized

参考：<https://baijiahao.baidu.com/s?id=1654344500475304827&wfr=spider&for=pc>

偏向锁：大多数情况，锁不存在多线程竞争。为了减少获得锁的代价，引入。线程获取锁的时候会把线程的id存储在对象头的MarkWord和栈帧锁记录中，这样再次获取锁只要测试MarkWord是否存储着当前线程id是否一致即可。如果测试不成功，测试MarkWord中的偏向锁标识是否为1，为1则用CAS获取，不为1则尝试使用CAS将对象头的偏向锁指向当前线程。

轻量级锁：把MarkWord复制到栈帧中存储，同时CAS替换MarkWork为指向对应栈帧的指针，替换成功获取锁，失败则自旋，自旋一定次数后升级到重量级锁。

### 运行时数据区

1. 堆：存储对象实例和数组

   堆可细分为Young Gen和Old Gen，Young Gen分为Eden、from survivor和to survivor，默认8：1：1。

   JVM每次只使用Eden和其中的一块Survivor区来服务对象。

   堆区的虚拟机参数配置：

   -Xms:初始堆大小

   -Xmx:最大堆大小

   -Xmn:年轻代大小

   -XXSurvivorRatio:年轻代中Eden区和Survivor区的大小比值

   ​

2. 虚拟机栈：存储栈帧，栈帧是对应方法的内存模型，包含了局部变量表， 操作数栈，动态链接和方法出口。-Xss调整栈的大小。

3. 本地方法栈：类似虚拟机栈，但是里面的方法是native的

4. 程序计数器：相当于字节码执行的行号指令器。（唯一一个没有OOM情况的区域）

5. 方法区：保存被加载的类的信息和常量、静态变量、即时编译器编译后的代码。

   （JDK1.7以后，字符串常量池已经被移出方法区了）



### jstack

jstack可以定位哪些问题？ <https://www.cnblogs.com/chenpi/p/5377445.html>

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

### 字节码

一般通过 javac xxx.java 编译java文件->class文件，再通过javap -c xxx.class反编译生成

## IO

### Netty

三个优点：

1. 高并发，基于NIO开发的网络通信框架，对比BIO并发性能提升了很多。
2. 传输快，传输基于零拷贝实现，减少不必要的内存拷贝，传输效率高
3. 封装好，封装了NIO的很多操作细节，提供了易用的接口调用

#### Netty的心跳机制

IdleStateHandler

<https://blog.csdn.net/u013967175/article/details/78591810>

#### Netty的零拷贝

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

### mysql架构图

![img](https://www.linuxidc.com/upload/2018_11/181121105137362.png)

非聚簇索引=辅助索引

### Myisam和Innodb区别

myisam不支持事务，而innodb支持事务。

myisam只有表级锁，而innodb支持表、行级锁

容灾性差、而innodb有redo log，用于容灾恢复

InnoDB是聚集索引，使用B+树作为索引结构，数据文件和（主键）索引绑在一起，必须要有主键，通过主键索引效率很高。辅助索引查找一般要进行回表查询，主键过大会导致其他索引页很大。MyISAM是非聚集索引，也是B+树结构，但是索引和数据文件是分离的，索引保存的是数据文件的指针。

参考：<https://blog.csdn.net/qq_35642036/article/details/82820178>

### InnoDB

InnoDB一个B+树可以放多少行数据？大概2千万行。最小存储单元是页，每个页默认是16K大小，可以通过 innodb_page_size进行设置。

计算过程

主键 bigint 8字节+指针 6字节 =14字节 。
根页 16k/14=1170
一行数据1k,每页存16k/1k=16
三层b+树应该是 1170*1170*16=21902400

参考： <https://www.jianshu.com/p/3578beed5a68>

### 解决幻读

<https://zhuanlan.zhihu.com/p/83584160>

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

### count(1)和count(*)

参考：<https://www.cnblogs.com/vandusty/p/12248605.html>

### SQL题

成绩表，三个字段：姓名、课程、成绩，求课程平均成绩大于85的学生姓名和平均成绩

```SQL
select n , sc from (select avg(score) as sc,name as n from tb group by n having sc>85 ) 
```

### drop、truncate、delete区别

1. delete是每次从表中删除一行，并且同时将改行的删除操作作为事务记录在日志中以便回滚。
2. truncate 一次性删除表中所有的数据并不记录日志，无法恢复，但是保存表的结构。删除过程不会激活触发器，速度快。
3. drop将表锁占用的空间全释放掉。

### 触发器

触发器是与表有关的数据库对象，在满足定义条件时触发，并执行触发器中定义的语句集合。

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

### join的执行过程（未完成）



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

#### curl

执行http请求 如 curl  localhost:8080/cover_file/5126102850063143942

#### 统计当前文件夹下面.jpg文件的数量

ls -l | grep '.*\.jpg' | wc -l

## 操作系统

### 死锁的四个必要条件

1. 互斥
2. 请求和保持
3. 循环等待
4. 不可抢占

虚拟内存和物理内存和分页管理这部分建议微信公众号搜 小林coding 。有文章讲解特别详细。

虚拟内存和物理内存的映射关系和工作原理：

<https://blog.csdn.net/don_chiang709/article/details/89087709>

### 虚拟地址技术、分页、分段

虚拟地址技术解决了各个进程同时运行时对物理内存的访问冲突，为每个进程单独分配一套独立的虚拟地址，映射到不同的物理内存，实现了进程之间的内存隔离。通过MMU 内存管理单元实现的虚拟地址到物理地址的映射。

内存管理的方式：分段、分页。



程序是若干个逻辑分段组成的----代码段，数据段，栈段，堆段等。不同的段属性不同，所以要进行分段管理。分段机制下虚拟地址主要分为两部分----段选择子（段号和标志位）和段内偏移量，根据段表可以找对应的物理地址。

分段管理存在的问题：内存碎片和内存交换的效率低。

为了解决这个问题，提出分页管理机制。分页是把整个虚拟和物理内存空间切成一段段固定尺寸的大小----页，两者通过页表进行映射。Linux页的大小4k，消除了内存外碎片，提高了内存使用率，同时内存交换的效率相对较高。



**两者的区别：**

1. 页是信息物理单位，主要是为了实现内存离散分配，解决外碎片，提高内存的利用率。而段是信息的逻辑单位，含有一组意义相对完整的信息，是为了更好的满足用户需求。
2. 页大小固定，由系统确定，逻辑地址=页号+页内地址。段大小不固定，取决于用户编写的程序。
3. 分页的作业地址空间是一维的，分段是二维的，再标识一个地址时候，需要段名+段内地址。



### 进程通信

1. 信号

   进程通过信号进行通信，用于用纸接受进程的某个事件已经发生。如kill -9 pid 就是向pid进程发起结束进程的信号

2. 管道。内核中的一串缓存，分为有名管道和匿名管道。匿名管道用于父子进程的通信，而有名管道用于无亲缘关系的进程通信。常用的ps -aux|grep pid中的竖杠就是匿名管道。但是管道中的数据是无格式的流。

3. 消息队列。消息队列是存在内核中的一个消息链表结构，进程可以生产消息添加到链表也可以消费消息，消费后的消息会从链表中移除，链表消息的结构体是由用户自定义的。但是消息队列通信过程中，存在用户态和内核态的数据拷贝开销，不适合大数据传输。

4. 共享内存。通过将不同进程的虚拟地址映射到同一块内存区域，实现进程之间的共享，不用再进行内核态和用户态的拷贝。

5. 信号量。整型的计数器，不是用来缓存进程间通信的数据，而是用于控制进程之间的同步和互斥。通过P,V操作来控制进程的同步和互斥。

6. 信号。是进程间唯一的异步通信机制。可通过kill -l查看所有信号。信号包括硬件来源和软件来源，硬件来源如ctrl+c（产生SIGINT信号，终止进程），软件来源如kill -9 pid（产生SIGKILL信号，立即结束进程）。

7. Socket。用于不同主机的进程之间的通信。

### 进程调度算法

1. 先来先服务   短进程响应时间过长
2. 短任务优先    长进程会产生饥饿现象
3. 高响应比优先   综合考虑等待时间和要求服务时间。 响应比=（等待时间+要求服务时间）/要求服务时间
4. 时间片轮转    
5. 短作业有限
6. 最短剩余时间优先
7. ​

## 计算机网络

### TCP可靠性保证

1. 检验和。计算内容包括TCP首部及数据部分。计算方法为：在发送方将整个报文段分为多个16位的段，然后将所有段进行反码相加，将结果存放在检验和字段中，接收方用相同的方法进行计算，如最终结果为检验字段所有位是全1则正确（UDP中为0是正确），否则存在错误。

2. 序列号和确认应答。TCP传输时将每个字节的数据都进行编号，接收方收到后会对传输方进行确认应答。

3. 超时重传。

4. 流量控制。

5. 拥塞控制。慢启动，拥塞避免；快重传，快恢复。

   **慢启动、拥塞避免：**刚开始时，发送方不知道网络的承载能力，如果一开始就发送大量数据，容易造成网络拥堵和丢包问题。刚开始时定义发送窗口为1，向网络中发送数据包，每次发送数据前，与接收方的反馈窗口大小进行比较，取最小值作为实际发送的窗口。执行慢启动算法，发送窗口呈指数增长，达到门限值ssthresh时执行拥塞避免算法，发送窗口线性增长。

   当出现网络拥塞的时候，把门限值ssthresh降为当前发送窗口的一半。

   **快重传、快恢复：**快速重传要求接收方在收到一个失序报文后立即发出重复确认，（为的是使发送方提早知道有报文段没有达到对方），而不要等自己发送数据的时候捎带确认。规定：发送方连续收到3个重复确认就应当立即重传对方未收到的报文段，不必等到超时重传计数器时间到期。快恢复，在网络发生拥塞时，执行乘法减小，把慢开始门限减半，执行拥塞避免算法，使拥塞窗口缓慢增大。

参考：<https://www.jianshu.com/p/42dbcd39c3e7>



### HTTP状态码

200 请求成功，并且返回结果

301 永久重定向。客户端保存新的链接并且向新的链接发出请求，返回结果。

302 临时重定向。	资源临时移动，客户端使用原有的uri。

400 客户端请求语法错误。

404 请求失败，找不到资源。

500 服务器错误。

502 Bad Gateway充当网关或代理的服务器，从远端服务器接收到了一个无效的请求

503 服务器过载或者维护，无法解决当前的请求。

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

### SSL过程

参考：<https://blog.csdn.net/weixin_42600398/article/details/104128676>

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

### 数据传输流程

<https://blog.csdn.net/xiayun1995/article/details/82380819>

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

## 中间件和框架

<<<<<<< HEAD
### SpringBoot自动装配

SpringBoot启动类上的注解@SpringBootApplication，这个注解包含了@SpringBootConfiguration和@ComponentScan和@EnableAutoConfiguration三个注解。自动装配的核心在于注解@EnableAutoConfiguration，它包含关键注解@Import({AutoConfigurationImportSelector.class})，这个注解会将AutoConfigurationImportSelector.class类加载到容器中，这个类中的getCandidateConfigurations方法里面通过SpringFactoriesLoader.loadFactoryNames()扫描所有具有`META-INF/spring.factories`的`jar`包（ spring.factories 我们可以理解成 `Spring Boot` 自己的 `SPI` 机制）。 `spring-boot-autoconfigure-x.x.x.x.jar`里就有一个spring.factories文件。`spring.factories`文件由一组一组的`Key = value`的形式，其中一个`key`是EnableAutoConfiguration类的全类名，而它的value是一个以`AutoConfiguration`结尾的类名的列表，有`redis、mq`等这些类名以逗号分隔。

参考：<https://zhuanlan.zhihu.com/p/163685081>

### Spring启动过程

首先实例化SpringApplication对象，在它的构造函数中会对  初始化上下文的各种接口ApplicationContextInitializer和监听器ApplicationListener进行初始化。（是在spring初始化之前完成的，不依赖于spring容器的加载）



分析 ：<https://www.jianshu.com/p/603d125f21b3>

springboot启动结构图 ：<https://www.processon.com/view/link/59812124e4b0de2518b32b6e>
=======
### SpringBoot


>>>>>>> 08b2779e424bf3cea8b620350127f757559d1d39

### Spring

#### Bean生命周期

参考：<https://www.jianshu.com/p/38032b0b9869>

1. 实例化Bean对象。createBeanInstance()

2. 为Bean设置相关的属性和依赖。populateBean()

3. 初始化，包括检查Aware 接口的依赖注入、BeanPostProcessor 在初始化前后的处理以及 InitializingBean 和 init-method 的初始化操作。initializeBean()

4. 销毁，检查Destruction相关回调接口、是否实现DisposableBean接口、是否配置自定义的destory-method。registerDisposableBeanIfNecessary()

   ```java
   // AbstractAutowireCapableBeanFactory.java
   protected Object doCreateBean(final String beanName, final RootBeanDefinition mbd, final @Nullable Object[] args)
       throws BeanCreationException {

       // 1\. 实例化
       BeanWrapper instanceWrapper = null;
       if (instanceWrapper == null) {
           instanceWrapper = createBeanInstance(beanName, mbd, args);
       }

       Object exposedObject = bean;
       try {
           // 2\. 属性赋值
           populateBean(beanName, mbd, instanceWrapper);
           // 3\. 初始化
           exposedObject = initializeBean(beanName, exposedObject, mbd);
       }

       // 4\. 销毁-注册回调接口
       try {
           registerDisposableBeanIfNecessary(beanName, bean, mbd);
       }

       return exposedObject;
   }
   ```

   ​

### Redis

#### 三种集群模式和主从同步

<https://www.cnblogs.com/51life/p/10233340.html>

#### 持久化

1. RBD。保存数据快照，有三种机制：save，bgsave，自动化。

   save会阻塞当前服务器进程，使得不能处理其他命令。

   bgsave会在后台异步执行快照操作，通过fork()产生子进程，负责持久化。

   自动化触发是在redis.conf中进行配置，比如“save m n”。表示m秒内数据集存在n次修改时，自动触发bgsave。

2. AOF。记录每条变更数据的操作指令，默认是每秒将写操作日志追加到AOF文件中。

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

作用：解耦、异步、削峰

#### **如何防止重复消费？**

1. 同步提交，会有性能影响。
2. 消息使用唯一id标识-->落表（主键或者唯一索引避免重复）或者选择唯一主键存储到redis，若存在则不处理，不存在则插入后处理。

#### **如何防止消息丢失？**

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

### 项目

断点续传 https://github.com/niumoo/down-bit