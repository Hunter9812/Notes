# Hadoop

集群启动/停止方式总结

- 整体启动/停止HDFS

  start-dfs.sh/stop-dfs.sh

  start-yarn.sh/stop-yarn.sh

- 各个服务组件逐一启动/停止

  hdfs --daemon start namenode/datanode/secondarynamenode

  yarn --daemon start namenode/datanode/secondarynamenode

HA启动

- stop-dfs.sh

- 三台机器

  zkServer.sh start

- 第一次启动需要格式化zk

  hdfs zkfc -formatZK

- 启动hdfs

  start-dfs.sh

-



# HDFS Shell命令

hadoop fs与hdfs dfs的命令的使用是相似的，本实验使用的是hdfs dfs命令，所有命令的操作都是在hadoop用户下进行。

- mkdir：创建文件夹

    Synopsis：`hdfs fs -mkdir [-p]`

    接受路径指定的uri作为参数，创建这些目录。其行为类似于Unix的mkdir -p，它会创建路径中的各级父目录。

- touchz：新建文件

    Synopsis：`hdfs fs -touchz URI [URI …]`

    当前时间下创建大小为0的空文件，若大小不为0，返回错误信息。

- ls：列指定目录文件和目录

    Synopsis：`hdfs dfs -ls [-d][-h][-R]`

    表一ls命令选项和功能

    | 选项 | 功能说明                                                 |
    | ---- | -------------------------------------------------------- |
    | -d   | 返回paths                                                |
    | -h   | 按照KMG数据大小单位显示文件大小，如果没有单位，默认认为B |
    | -R   | 级联显示paths下文件，这里paths是个多级目录               |

- rm：删除目录和文件

    hdfs dfs -rm [-f] [-r|-R] [-skip Trash]

    表二rm命令的选项和功能

    | 选项       | 说明                                         |
    | ---------- | -------------------------------------------- |
    | -f         | 如果要删除的文件不存在，不显示提示和错误信息 |
    | -r \| R    | 级联删除目录下的所有文件和子目录文件         |
    | -skipTrash | 直接删除，不进入垃圾回车站                   |

# MapReduce

> MapReduce 的开发一共有八个步骤,其中 Map阶段分为2个步骤，Shuffle阶段4个步骤，Reduce阶段分为2个步骤

Map阶段2个步骤

1. 设置InputFormat类,将数据切分为Key-Value(K1和V1)对,输入到第二步
2. 自定义Map逻辑,将第一步的结果转换成另外的Key-value (K2和V2）对,输出结果

Shuffle阶段4个步骤

3. 对输出的 Key-Value对进行分区
4. 对不同分区的数据按照相同的Key 排序
5. (可选)对分组过的数据初步规约,降低数据的网络拷贝
6. 对数据进行分组,相同Key的value放入一个集合中

Reduce阶段2个步骤

7. 对多个Map任务的结果进行排序以及合并,编写Reduce 函数实现自己的逻辑,对输入的Key-value进行处理,转为新的Key-Value (K3和V3) 输出
8. 设置OutputFormat处理并保存Reduce输出的Key-Value数据


分区、排序、规约、分组

