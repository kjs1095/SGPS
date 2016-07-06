
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
  -ifs , -inputfiles
  -mcfg , -machineconfigfile
  -jc, -jobconfiguration
  -log4jconf, -log4jconfig
  -sub, -subgraph
  -dir, -directed
  -batch, -batchmode
  -w, -window
