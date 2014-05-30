# Administering Hadoop
## HDFS
### Persistent Data Structures
#### Namenode Directory Structure

  {dfs.name.dir}/current/VERSION
 						/edits
						/fsimage
						/fstime

**VERSION** is a Java properties file that contains information about the version of HDFS:
	#Tue Mar 10 19:21:36 GMT 2009
	namespaceID=134368441
	cTime=0
	storageType=NAME_NODE
	layoutVersion=-18

**layoutVersion** defines the version of HDFS persistent data structures. Whenever the layout changes, the version is decremented

**namespaceID** Unique identifier for the filesystem