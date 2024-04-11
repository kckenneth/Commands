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
