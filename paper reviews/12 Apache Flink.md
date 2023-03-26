

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| Apache Flink™: Stream and Batch Processing in a Single Engine |
| 2015 IEEE                                                    |
| CS  341                                                      |

## summary

1. This paper presents Apache Flink, a distributed data processing engine designed to handle stream and batch processing workloads in a single system.
2. This paper discusses several key features of Flink, including its support for complex event processing and fault tolerance mechanisms.
3. Flink is optimized for high throughput and low latency data processing.

## advantage

1. It allows users to process data in real-time as it is generated while supporting the efficient processing of large volumes of historical data.
2. Flink is designed to be fault tolerant with *exactly-once* processing guarantees.
3. It is open source.
4. It supports very high throughput and low event latency at the same time.

## drawback

1. This paper doesn't provide enough experiment to show the performance of Flink.
2. It considers batch as special streaming. So it does not have the same good throughput as Spark at batch processing.
1. The state checkpoint is very complex and hard to understand.

## Justification

1. Flink is the only system incorporating i) a distributed dataflow runtime that exploits pipelined streaming execution for batch and stream workloads, ii) exactly-once state consistency through lightweight checkpointing, iii) native iterative processing, iv) sophisticated window semantics, supporting out-of-order processing.
2. Flink's programming model is designed to be easy to use and developer-friendly, with a range of APIs and libraries that simplify the development of data processing applications.
3. Flink can be easily integrated with other data processing frameworks such as Apache Hadoop and Apache Storm, making it a good choice for organizations with existing data processing infrastructure. This allows for a more flexible and customizable data processing architecture.



展示

##### why flink? 

stream first priciple

real streaming processing engine. consider batch as a 特殊streaming. 

##### stack

三层, clear abstraction. deploy, core, api 

api,  生成运行计划. 

tramsormation.  program  生成stream data flow

source -> sink,  可以是HDFS files, kafka data, text.  csv, hadoop. HBase. 

数据- > flat map, ma, keyby, window 等操作,  -> HDFS 

client  : 提交job

jobmanage : 管理task manger, 

resource manager,  调度分配 allocate, scheduling 

task manager: 一个应用可以分解给多个task manager 来计算. 

每个work 也叫task manager都是一个JVM, 可能多线程执行subtask.   work有多个task slot, taskslot 资源的子集. 比如可以把内存分成三份, 3个slot. 但是不分CPU . 就是3个subtask share same JVM, share TCPconnection和heartbeat. 

Operation chain.  Other can parallel, but  parallisim of sink is one .

#### windows

time driven or data driven ,eg.   every 100 element. 

tumbling windows,  times do not overlap 

sliding windows, windows size changes ,  time overlap / 

session window,   

#### barrier

CL 算法,  barrier inject into flow . barrier, don't interrupt flow of stream, so lightweight.  

checkpointcordinator ,send barrier to all source op of streaming application.

source operation create a snapshot of his current status  ,persistent . notify coordinator, it created. 

broadcast barrier to all downstream operators. and resume data processing 

until barrier sent to sink op . 

Coorditor receive all report. 

