# 个人项目：论文查重

| 这个作业属于哪个课程 | https://edu.cnblogs.com/campus/gdgy/CSGrade22-34             |
| -------------------- | ------------------------------------------------------------ |
| 这个作业要求在哪里   | https://edu.cnblogs.com/campus/gdgy/CSGrade22-34/homework/13229 |
| 这个作业的目标       | 设计和实现一个简单的论文查重算法，用于检测抄袭版论文与原文之间的相似度 |
| GitHub地址           | https://github.com/fw-1208/https-github.com-fw-1208/tree/main/3222004721 |

# PSP表格

| PSP2.1                                | Personal Software Process Stages      | 预估耗时（分钟） | 实际耗时（分钟） |
| ------------------------------------- | ------------------------------------- | ---------------- | ---------------- |
| Planning                              | 计划                                  | 30               | 15               |
| Estimate                              | 估计这个任务需要多少时间              | 1335             | 1295             |
| Development                           | 开发                                  | 300              | 270              |
| Analysis                              | 需求分析 (包括学习新技术)             | 110              | 60               |
| Design Spec                           | 生成设计文档                          | 60               | 30               |
| Design Review                         | 设计复审                              | 40               | 20               |
| Coding Standard                       | 代码规范 (为目前的开发制定合适的规范) | 45               | 35               |
| Design                                | 具体设计                              | 180              | 240              |
| Coding                                | 具体编码                              | 230              | 300              |
| Code Review                           | 代码复审                              | 60               | 80               |
| Test                                  | 测试（自我测试，修改代码，提交修改）  | 30               | 30               |
| Reporting                             | 报告                                  | 120              | 150              |
| Test Repor                            | 测试报告                              | 60               | 30               |
| Size Measurement                      | 计算工作量                            | 30               | 30               |
| Postmortem & Process Improvement Plan | 事后总结, 并提出过程改进计划          | 45               | 30               |
|                                       | 合计                                  | 1360             | 1310             |

# 一.需求分析

1.1 原需求

题目：论文查重

描述如下：

设计一个论文查重算法，给出一个原文文件和一个在这份原文上经过了增删改的抄袭版论文的文件，在答案文件中输出其重复率。

- 原文示例：今天是星期天，天气晴，今天晚上我要去看电影。
- 抄袭版示例：今天是周天，天气晴朗，我晚上要去看电影。

要求输入输出采用文件输入输出，规范如下：

- 从**命令行参数**给出：论文原文的文件的**绝对路径**。
- 从**命令行参数**给出：抄袭版论文的文件的**绝对路径**。
- 从**命令行参数**给出：输出的答案文件的**绝对路径**。

我们提供一份样例，课堂上下发，上传到班级群，使用方法是：orig.txt是原文，其他orig_add.txt等均为抄袭版论文。

注意：答案文件中输出的答案为浮点型，精确到小数点后两位

1.2 设计思路

![img](https://img-community.csdnimg.cn/images/f99cfe6d5e6d4684a72ebafe6b009ac9.png)

# 二.开发环境

开发环境：IntelliJ IDEA Community Edition 2024.1.1

开发语言：Java JDK version 1.8

三.模块接口的设计实现

## 三.整体设计

3.1 整体流程图

![image](https://github.com/user-attachments/assets/946f0cce-a60d-4b88-ad02-865a2bdfd37b)


3.2 核心算法

此论文查重程序主要依靠的是SimHash和海明距离。
具体的算法分析和实现可以参考使用SimHash以及海明距离判断内容相似程度。

3.2.1 SimHash算法
SimHash主要是将文章分词并且将每个词都附上权重，然后将分词通过Hash算法计算出哈希值，将哈希值进行加权后把所有值相加，得到一序列串，最后把这个序列串简化为1、0组成的序列。

3.2.2 海明距离
通过比较差异的位数就可以得到两串文本的差异，差异的位数，称之为“海明距离”，通常认为海明距离<3的是高度相似的文本。

# 四.模块接口部分的性能改

总览

![image](https://github.com/user-attachments/assets/9bc477f5-9180-4ed6-aeb8-2fe9307339cb)
方法调用情况

![image](https://github.com/user-attachments/assets/02815276-3d3e-4d9f-859c-295516fd0aaa)







# 五.模块部分单元测试展示

部分测试代码

public class MainTest {
    @Test
    public void origAndAllTest(){
        String[] str = new String[6];
        str[0] = IOUtils.read("D:/test/orig.txt");
        str[1] = IOUtils.read("D:/test/orig_0.8_add.txt");
        str[2] = IOUtils.read("D:/test/orig_0.8_del.txt");
        str[3] = IOUtils.read("D:/test/orig_0.8_dis_1.txt");
        str[4] = IOUtils.read("D:/test/orig_0.8_dis_10.txt");
        str[5] = IOUtils.read("D:/test/orig_0.8_dis_15.txt");
        String ansFileName = "D:/test/ansAll.txt";
        for(int i = 0; i <= 5; i++){
            double ans = HammingUtils.getSimilarity(SimHashUtils.getSimHash(str[0]), SimHashUtils.getSimHash(str[i]));
            IOUtils.write(ans, ansFileName);
        }
    }
}

代码覆盖率

![img](https://i-blog.csdnimg.cn/blog_migrate/1e05614302ab93b9a8eef1e1896134c1.png)

![img](https://i-blog.csdnimg.cn/blog_migrate/3664b0d4163186aea69aef8e4ebfabf0.png)

![img](https://i-blog.csdnimg.cn/blog_migrate/ef1aeb96fa05ac4003ff1219b945a19a.png)



测试结果

![img](https://i-blog.csdnimg.cn/blog_migrate/0c402711bb735efb946b4d3b0317d64d.png)

结果文件

![image](https://github.com/user-attachments/assets/e9deef23-4d2a-45d1-8a04-8bd20956f9e2)






# 六.异常处理

当文本过短无法提取关键字，则抛出异常。







