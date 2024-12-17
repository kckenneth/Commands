### Hadoop

For running oozie job in hadoop, the mapper script doesn't need to be a full path, it's just the <file> needs to be a full path. 

```
  <action name="extract_all">
    <map-reduce>
      <streaming>
        <mapper>extract_everything.py</mapper>
        <reducer>/bin/cat</reducer>
      </streaming>
      <configuration>
        <property><name>mapreduce.map.memory.mb</name><value>20000</value></property>
        <property><name>mapred.input.dir</name><value>${wf:actionData('getLatestPath')['latestPath']}/*</value></property>
        <property><name>mapred.output.dir</name><value>${output}</value></property>
        <property><name>mapred.reduce.tasks</name><value>20</value></property>
      </configuration>
      <file>${wfRoot}/scripts/extract_everything.py</file>
    </map-reduce>
    <ok to="deduplicate" />
    <error to="email_error" />
  </action>
```

### Check the content of .tgz file

```
hdfs dfs -copyToLocal /projects/xxx.tgz
vi xxx.tgz            # check the content or
tar -tf xxx.tgz | grep "apple.txt"
```

### Check hadoop space 

```
sudo -u qlasbld -s
hdfs dfs -du -h /projects/qlas

hdfs dfs -rm -r -skipTrash /projects/qlas/qlas_synonym/US/202212*
```

- checking cosmo feeds

```
hadoop fs -count -v -q -h /projects/search_platforms
       QUOTA       REM_QUOTA     SPACE_QUOTA REM_SPACE_QUOTA    DIR_COUNT   FILE_COUNT       CONTENT_SIZE PATHNAME
     488.3 K               0           300 T         275.1 T        3.0 K      485.3 K              8.3 T /projects/search_platforms
```

- deleting old feeds

```
hdfs dfs -rm -skipTrash  /projects/search_platforms/qp/datapush/data/stage/*/web/ftdict/qp-datafile-2023.*
```

