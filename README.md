# random_fast_notes


- SSH port forwarding, Redis

1. `ssh -L 6000:arteries-hot-events.yzirwe.clustercfg.use1.cache.amazonaws.com:6379 ec2-18-234-141-194.compute-  amazonaws.com`
2. on another terminal `Redis-cli -p 6000`

- Change Java version on local
```$ /usr/libexec/java_home -V

Matching Java Virtual Machines (3):
    12.0.2, x86_64:	"Java SE 12.0.2"	/Library/Java/JavaVirtualMachines/jdk-12.0.2.jdk/Contents/Home
    1.8.0_231, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
    1.8.0_202, x86_64:	"Amazon Corretto 8"	/Library/Java/JavaVirtualMachines/amazon-corretto-8.jdk/Contents/Home
```

then you can ```$ export JAVA_HOME=`/usr/libexec/java_home -v 1.8.0_231```


### project

- Create a Conda package
1. `conda-build .` current package, with meta.yaml, build.sh included
2. Conver to linux platform 
`conda convert --platform linux-64 ~/opt/anaconda3/conda-bld/osx-64/click-7.0-py37_0.tar.bz2 -o outputdir/`
3. `conda index .` current folder, folder should have a linux-64 subfolder with the built tar file
4. Move the contents to S3 bucket
5. `conda install "$NAME_OF_PACKAGE" -c "$PATH_TO_S3"`

- Use a conda env in a Dockerfile 

```
RUN curl -o ~/miniconda.sh -O  https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh  \
 && chmod +x ~/miniconda.sh \
 && ~/miniconda.sh -b -p /opt/conda \
 && rm ~/miniconda.sh \
 && /opt/conda/bin/conda install aws-requests-auth -y -c conda-forge
RUN /opt/conda/bin/conda clean -ya

## activate myenv
#COPY environment.yaml /notebooks
RUN /opt/conda/bin/conda env create -f environment.yaml
RUN echo "source activate myenv" > ~/.bashrc
ENV PATH /opt/conda/envs/myenv/bin:$PATH
```

- SSH to bastion
1. `ssh-add`
2.  `ssh -A <bastion>`
