# TDP HBase Notes

The version 2.4.17-1.0 of HBase is based on the `branch-2.4` tag of the Apache [repository](https://github.com/apache/hbase/tree/branch-2.4).

## Jenkinfile

The file `./Jenkinsfile-sample` can be used in a Jenkins / Kubernetes environment to build and execute the unit tests of the Spark project. See []() for details on the environment.

## Making a release

```
mvn clean package assembly:single -DskipTests -Dhadoop.profile=3.0 -s tdp/settings.xml
```

The command generates a `.tar.gz` file of the release at `./hbase-assembly/target/hbase-2.4.17-TDP-1.0-bin.tar.gz`.

The command `-s tdp/settings.xml` which is not obligatory mirrors all repositories with maven-central and therefore increases downloading speed since maven does not search in unexisting repositories.

Replace `package` for `install` in the above command to ensure built package is available in your local maven repository post build.

## Testing parameters

```
mvn test -Dhadoop.profile=3.0
```

- -Dhadoop.profile=3.0: Builds with Hadoop 3 (Hadoop TDP version is set with `hadoop-three.version`)
- --fail-never: Does not interrupt the tests if one module fails

## Test execution notes

See `./test_notes.txt`

## Build notes

Commit `ab28cf08e34907d1dabe0fdb001841ee287acb82` adds extra options to HBase HBCK. A backport from HBase 2.4.
