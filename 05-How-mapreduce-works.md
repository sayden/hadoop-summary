# How MapReduce Works

Prior to 0.23, setting `mapred.job.tracker` to **local**  the local job runner is used. YARN uses `mapreduce.framework.name` which takes the values **local**, **classic** and **yarn**

## Classic MapReduce (MapReduce 1)

![alt text](image-09.png)

1. Client submits job
2. **JobTracker** coordinates job run
3. **TaskTracker** run the tasks that the job has been split into
4. The **HDFS** is used for sharing job files.

**submit()** method on **Job** creates an internal **JobSummiter** and calls **submitJobInternal()** on it:

1. Asks jobtracker for new job ID calling **getNewJobId()** on **JobTracker**
2. Checks output dir
3. Computes input splits
4. Copies the needed resources (JAR, config file...). The JAR is copied with high replication factor set by `mapred.submit.replication` property (defaults to 10)
5. Tells the **JobTracker** the job is ready calling **submitJob()**

### Job Initialization

**JobTracker** enqueue the job and creates a list of tasks retrieving the input splits to create one map for each split. The number of reduce tasks to create is in `mapred.reduce.tasks` or set by the **setNumReduceTasks()**. Also a *job setup tasks* and a *job cleanup task* are run by the **TaskTrackers** to setup the job and cleanup after reduce tasks are completed. **OutputCommiter** the code to run

### Task Assignment

**TaskTrackers** tells JobTracker they are alive and if they are ready throught *heartbeat* calls and they have a fixed number of slots for map and reduce tasks. Map slots has priority over reduce ones.

The **JobTracker** picks a map task whose input split is as close as possible to the tasktracker If possible it will be *data-local*. Alternatively, *rack-local* (same rack). To choose a reduce it simply takes the next in the queue.

### Task Execution

