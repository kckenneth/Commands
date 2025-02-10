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

### Check local home directory quota 

```
/gridtools/generic/bin/homedir-quota
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 1.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 2.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 3.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 4.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 5.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 6.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 7.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 8.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 9.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 10.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 11.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 12.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 13.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 14.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 15.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 16.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 17.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 18.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 19.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 20.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 21.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 22.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 23.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 24.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 25.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 26.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 27.
Use of uninitialized value $dev in string eq at /gridtools/generic/bin/homedir-quota line 19, <QUOTA> line 28.
Use of uninitialized value $dev in concatenation (.) or string at /gridtools/generic/bin/homedir-quota line 25.
Quota for kchen08 on /homes/kchen08 ()
space quota: 10.00 GiB
space used: 5.12 GiB (51.2%)
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

