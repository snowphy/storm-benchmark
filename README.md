# Storm Benchmark [![Build Status](https://travis-ci.org/intel-hadoop/storm-benchmark.svg?branch=master)](https://travis-ci.org/intel-hadoop/storm-benchmark?branch=master)

## How do we measure storm performance

The benchmark set contains 9 workloads. They fall into two categories. The first category is "simple resource benchmark", the goal is to test how storm performs under pressure of certain resource. The second category is to measure how storm performs in real-life typical use cases.

 - Simple resource benchmarks:
    * wordcount, CPU sensitive
    * sol, network sensitive
    * rollingsort, memory sensitive

 - Typical use-case benchmark:
     * rollingcount
     * trident
     * uniquevisitor 
     * pageview
     * grep
     * dataclean
     * drpc

## How to use

This guide assumes a Storm cluster is already set up locally.

1. Build. 
   
  First, build storm-benchmark.
  ```bash
    git clone https://github.com/manuzhang/storm-benchmark.git
    mvn package
  ```

2. Run.

  ```bash
    bin/stormbench -storm ${STORM_HOME}/bin/storm -jar ./target/storm-benchmark-${VERSION}-jar-with-dependencies.jar -conf ./conf/sol.yaml -c topology.workers=2 storm.benchmark.tools.Runner storm.benchmark.benchmarks.SOL 
  ```
  
 * `-storm` directs stormbench to look for the storm command
 * `-jar` sets the benchmark jar with all the dependencies in 
 * `-conf` is for user to provide a yaml conf file like `storm/conf/storm.yaml`. Check the `storm-benchmark/conf` folder where conf files are already provided for existing benchmarks
 * `-c` allows user to set conf through command line without modifying conf files every time

 
3. Check.  The benchmark results will be stored at config path METRICS_PATH(default is: reports). It contains throughput data and latency of the whole cluster.
 
 The result of SOL contains two files

    1. `SOL_metrics_1402148415021.csv`. Performnace data.
    2. `SOL_metrics_1402148415021.yaml`. The config used to run this test.

## Supports

Please contact:

 - Manu Zhang: tianlun.zhang@intel.com
 - Sean Zhong: xiang.zhong@intel.com

## Acknowledgement

We use the SOL benchmark code(https://github.com/yahoo/storm-perf-test) from yahoo. Thanks. 
