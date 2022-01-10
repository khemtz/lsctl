#COMO INSTALAR LA APP

```
[root@azh1e1srels02 home]# mkdir pipelines
[root@azh1e1srels02 home]# cd pipelines/
[root@azh1e1srels02 pipelines]# git clone https://gitlab.digitalcoedevops.com/labs/aiops/lsctl.git
Cloning into 'lsctl'...
Username for 'https://gitlab.digitalcoedevops.com': cmartinez
Password for 'https://cmartinez@gitlab.digitalcoedevops.com':
remote: Enumerating objects: 16880, done.
remote: Counting objects: 100% (16880/16880), done.
remote: Compressing objects: 100% (11756/11756), done.
remote: Total 16880 (delta 3304), reused 16853 (delta 3299), pack-reused 0
Receiving objects: 100% (16880/16880), 343.91 MiB | 12.65 MiB/s, done.
Resolving deltas: 100% (3304/3304), done.
Checking out files: 100% (15380/15380), done.
[root@azh1e1srels02 pipelines]#
```

validar el PATH de JAVA_HOME

lo mejor es que tengas instalado java, aqui te paso el procedimiento para instalarlo:

##install JAVA

descarga la version de java 8 a tu home

```
mv /home/adm.chernandez@ad.hmshost.com/jre-8u261-linux-x64.tar.gz /root
```

como root:
```
mkdir /usr/java
mv /root/jre-8u261-linux-x64.tar.gz /usr/java
cd /usr/java
tar xvfz /usr/java/jre-8u261-linux-x64.tar.gz
mv jre1.8.0_261/ jre
update-alternatives --install /usr/bin/java java /usr/java/jre/bin/java 100
```

con esto el JAVA_HOME esta en /usr/java/jre


solo queda hacer un link 
```
[root@azh1e1srels02 bin]# ln -s /home/pipelines/lsctl/bin/lsctl /usr/local/bin/lsctl
[root@azh1e1srels02 bin]# ls -ltr /usr/local/bin/lsctl
lrwxrwxrwx. 1 root root 31 Jan 10 19:50 /usr/local/bin/lsctl -> /home/pipelines/lsctl/bin/lsctl
[root@azh1e1srels02 bin]#
```

#CORRER DIFERENTES VERSIONES DE LOGSTASH:

en caso de querer correr una nueva version de losgtash, solo es cuestion de bajar el .tar.gz de elastic.co/downloads
dentro de /home/pipelines/lsctl una vez descomprimido, solo es cuestion de renombrar el nombre a la version, por ejemplo 7.16.2



la configuracion del pipeline existe un archivo llamado lsctl.conf, solo es cuestion de ponerle la version

```
[root@azh1e1srels02 ~]# cd /home/pipelines/lsctl/
[root@azh1e1srels02 lsctl]# ls
7.15.1  bin  config  current  data  logs  lsctl
[root@azh1e1srels02 lsctl]# cd config
[root@azh1e1srels02 config]# ls
example
[root@azh1e1srels02 config]# cd example/
[root@azh1e1srels02 example]# ls
example.conf  jvm.options  log4j2.properties  logstash.yml  lsctl.conf  pipelines.yml.old  startup.options
[root@azh1e1srels02 example]# more lsctl.conf
LOGSTASH_VERSION="7.15.1"
[root@azh1e1srels02 example]#
```

solo es cuestion de que en es parametro le pongas la ersion en que quieras que se ejecute, puedes tambien ponerle current y hara referencia al link que existe donde hace referencia a la version mas actual
valida con un ls -ltr en /home/pipelines/lsctl

``` 
[root@azh1e1srels02 lsctl]# ls -ltr
total 4
drwxr-xr-x. 15 root root 4096 Jan 10 19:43 7.15.1
drwxr-xr-x.  3 root root   21 Jan 10 19:43 logs
drwxr-xr-x.  3 root root   21 Jan 10 19:43 data
lrwxrwxrwx.  1 root root    6 Jan 10 19:43 current -> 7.15.1
drwxr-xr-x.  3 root root   21 Jan 10 19:43 config
drwxr-xr-x.  2 root root   19 Jan 10 19:43 bin
lrwxrwxrwx.  1 root root   20 Jan 10 19:48 lsctl -> /usr/local/bin/lsctl
[root@azh1e1srels02 lsctl]#
```
