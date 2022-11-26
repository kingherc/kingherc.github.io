---
id: 30
title: The significance of performance for databases
date: 2014-12-24T20:04:08+01:00
permalink: /archives/30
categories:
  - Databases
  - Technology
---
It's been a long time since my last post..! I'm now in the middle of the fourth year. There's so much that has happened! I <a href="http://scholar.google.com/citations?user=TUcmoosAAAAJ">published</a> a lot, I programmed a lot, traveled a lot and now continuing my PhD in co-operation with <a title="SAP HANA students" href="http://scn.sap.com/docs/DOC-26824">SAP</a>, a big player in the market. I refined my software skills, especially my C++ and scripting skills. I also learned how to write scientifically, experiment, measure, and present results.

A big part of database research is about helping organizations and scientists to process data as quickly as possible. The significance of performance is enormous. Database vendors actually compete on performance (see for example <a href="http://www.tpc.org/">TPC</a> results). Thus, it is really important to optimize software so that it exploits resources to the maximum. For the developer, this means getting out of the mentality of producing code that "just works". We should not feel urged to write code quickly and sloppily. We need to take time to think about the quality of our code. Performance is a prominent aspect of quality. In this post, I'm explaining some basic facts about measuring performance and figuring out how to improve it.

### How to measure performance

What is performance? This is the first hard question you need to answer, and it's totally dependent on your situation. In databases, performance is typically measured with an objective metric such as **response time** or **throughput**. Response time is used for an experiment that involves a static load of work that needs to be processed. For example, executing a single batch of analytical queries. Throughput is typically used for more complex experiments that involve clients shooting up queries or transactions to the database. For example, there is a number of concurrent clients, each one issuing transaction-after-transaction, and we measure the total number of processed transactions per minute or hour.

Performance is typically **relative**. We compare the response time or throughput of different experiments, where we trigger various factors in order to gain insight into their effect on performance. For example, we may compare the response time of executing a query with different levels of parallelism, e.g., with 1 core, 2 cores, etc., up to all cores of our machine. Putting the observations on a 2D plot, with the # of cores on the x-axis, and response time on the y-axis, we can compare the speed-up depending on the # of cores utilized, which can give us an insight into how well the database can scale up the execution of a single query on a multi-core machine.

Results should also be **stable**. Meaning that for each data point we produce, we need to have run several iterations. After throwing away the few outliers, we produce the average and the standard deviation. A standard deviation of less than 5% is a good indication of stable results. In a few rare situations, we might be interested in plotting the whole distribution of observations to see if there is a pattern we need to understand.

### Finding the bottleneck(s)

Apart from measuring performance, we typically wish to understand how performance is affected in order to improve it. A first step is plotting how different factors affect performance, such as the number of concurrent queries or clients, the level of parallelism, the data size, the selectivity of queries, the database configuration (e.g. buffer pool size, optimizer scrutiny) etc. Of course, we also need to assess how much each factor affects performance, as we typically want to improve performance by focusing on optimizing the factors in the critical path of execution, and not factors affecting just 2% of performance. Continuing the previous example with the different levels of parallelism, if we observe a performance plateau in our 2D plot, this might hint that there is a bottleneck that prevents further parallelism.

At such a point where we observe an unexpected irregularity, such as the performance plateau, research comes alive. We need to squeeze our minds and think about the possible reasons for this plateau. For example, we might think about <a href="http://en.wikipedia.org/wiki/Amdahl%27s_law">Amdahl's law</a>, and figure out that our algorithms suffer from numerous serial parts that cannot be parallelized. Or, we might figure out that we suffer from a bottleneck. For example, parallelizing a simple main-memory scan on a multi-socket multi-core machine could run into a bottleneck of the memory bandwidth of a single socket. The key point is to have an open mind!

### Tools that can help you  

Apart from reasoning about the root cause, there are, fortunately, numerous tools that one can employ to drill down on bottlenecks and hotspots in the code. I've used a lot of them, and they helped immensely. Here are a few killer apps.

  * <a href="https://perf.wiki.kernel.org/index.php/Main_Page">Perf</a>  
    Perf is a quick and safe choice. It's highly integrated into linux and can measure all kinds of performance counters. For example, you can figure out which parts of your code have a high cache miss rate, and why.
  * <a href="https://software.intel.com/en-us/intel-vtune-amplifier-xe">Intel VTune Amplifier</a>  
    VTune is absolutely amazing in pinning down hotspots and measuring performance counters on machines with Intel processors. You can view a timeline of your experiment, see which parts of your code are parallelized, zoom in on parts of your experiment, and find out which functions took most of the processor time.
  * <a href="https://en.wikipedia.org/wiki/RotateRight_Zoom">Zoom</a>  
    The Zoom profiler is an alternative to VTune and provides a quick way to identify hotspots in your code.
  * <a href="https://software.intel.com/en-us/articles/intel-performance-counter-monitor-a-better-way-to-measure-cpu-utilization">Intel Performance Counter Monitor</a>  
    Intel PCM is a simple open-source tool to measure performance counters. This means you can edit the source code to measure any Intel hardware counter you wish, and gain more in-depth knowledge about the micro-architecture utilization of your experiment.
