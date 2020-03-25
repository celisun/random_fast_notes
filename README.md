# random_fast_notes

- SSH port forwarding for Redis

`ssh -L 6000:arteries-hot-events.yzirwe.clustercfg.use1.cache.amazonaws.com:6379 ec2-18-234-141-194.compute-1.amazonaws.com`
`Redis-cli -p 5000`

- Change local Java version
```$ /usr/libexec/java_home -V

Matching Java Virtual Machines (3):
    12.0.2, x86_64:	"Java SE 12.0.2"	/Library/Java/JavaVirtualMachines/jdk-12.0.2.jdk/Contents/Home
    1.8.0_231, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
    1.8.0_202, x86_64:	"Amazon Corretto 8"	/Library/Java/JavaVirtualMachines/amazon-corretto-8.jdk/Contents/Home
```

then you can ```$ export JAVA_HOME=`/usr/libexec/java_home -v 1.8.0_231```

- How to create a Conda package
1. `conda-build .` current package, with meta.yaml, build.sh included
2. Conver to linux platform 
`conda convert --platform linux-64 ~/opt/anaconda3/conda-bld/osx-64/click-7.0-py37_0.tar.bz2 -o outputdir/`
3. `conda index .` current folder, folder should have a linux-64 subfolder with the built tar file
4. Move the contents to S3 bucket
5. `conda install "$NAME_OF_PACKAGE" -c "$PATH_TO_S3"`
