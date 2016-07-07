
Dependency
--------------------
Following software should be installed before applying patch on [GPS](http://infolab.stanford.edu/gps/).

[HDFS](http://hadoop.apache.org) 
[RabbitMQ](https://www.rabbitmq.com)

Please make sure the authentication issue of RabbitMQ is solved.


Apply Patch
--------------------

```
$ cd trunk/src
$ git init
$ git add .
$ git commit -m "Initial commit"
$ git am --signoff < fix_empty_poster.patch
```

Compile
--------------------
Step 1. add all dependency jar files into trunk/libs

Step 2. revise compile script and manifest file

```
$ vim trunk/local-master-scripts/make_gps_node_runner_jar.sh
$ vim trunk/local-master-scripts/manifest.txt
```

Step 3. execute compile script

```
$ cd trunk/local-master-scripts
$ sh make_gps_node_runner_jar.sh
```


Deploy & Execute
--------------------
Step 1. tar files

```
$ cd trunk/local-master-scripts
$ sh make_gps_tar_gz.sh
```

Step 2. deploy tar files to all workers and untar

```
$ cd trunk/master-scripts
$ sh copy_and_untar_gps_tar_to_slaves.sh [num_of_machines]
```

Step 3. launch job by executing script

```
$ cd trunk/master-scripts
$ sh start_gps_nodes.sh [num_of_workers] [job_name] "[job_config_arguments]"
```

job arguments:
  -ifs FILEPATH:string, -inputfiles FILEPATH:string
						File path of data graph on HDFS
  -mcfg FILEPATH:string, -machineconfigfile FILEPATH:string
						File path of machine configuration on HDFS 
  -jc , -jobconfiguration
						Job configuration class
  -log4jconf FILEPATH:string, -log4jconfig FILEPATH:string
						File path of log4j configuration
  -sub boolean, -subgraph boolean
						True for subgraph-centric, False for vertex-centric
  -dir boolean, -directed boolean
						True for directed graph, False for undirected graph
  -batch boolean, -batchmode boolean
						True for running batch algorithm at the beginning of each window, False for incremental algorithm
  -w SECOND:int, -window SECOND:int
						Window size in second
