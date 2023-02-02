# Hadoop Cluster with Spark Set up

    Hadoop 3.2.1 Multi Node Cluster, Ubuntu 20.04

    What is Hadoop?

    “open-source software for reliable, scalable, distributed computing”, this means that is a framework for distributed processing.

    It’s simply several computers working together in order to improve processing power and assure decentralize operations.

    What do you need to start the set-up?

    I will use Ubuntu Server 20.04. The recommended space on your computer would be 24GB.

## Index
- [Step 1.  VMware Workstation pro 16 Network Setting](#Step-1-VMware-Workstation-pro-16-Network-Setting)
- [Step 2.  Install ssh](#Step-2-Install-ssh)
- [Step 3.  Install pdsh](#Step-3-Install-pdsh)
- [Step 4.  Set pdsh environment to ssh](#Step-4-Set-pdsh-environment-to-ssh)
- [Step 5.  Generate a SSH key](#Step-5-Generate-a-SSH-key)
- [Step 6.  Clone the key into authorized_keys files](#Step-6-Clone-the-key-into-authorized_keys-files)
- [Step 7.  Install Java 8](#Step-7-Install-Java-8)
- [Step 8.  It’s time to download and install Hadoop](#Step-8-It’s-time-to-download-and-install-Hadoop)
- [Step 9.  Set up Hadoop](#Step-9-Set-up-Hadoop)
- [Step 10.  Move the hadoop directory to our user local fileh](#Step-10-Move-the-hadoop-directory-to-our-user-local-file)
- [Step 11.  Set up hadoop path](#Step-11-Set-up-hadoop-path)
- [Step 12.  Create a specific user for Hadoop](#Step-12-Create-a-specific-user-for-Hadoop)
- [Step 13.  Clone the primary machine in order to create two secondary machines](#Step-13-Clone-the-primary-machine-in-order-to-create-two-secondary-machines)
- [Step 14.  Change hostnames](#Step-14-Change-hostnames)
- [Step 15.  Identify machine’s ip](#Step-15-Identify-machine’s-ip)
- [Step 16.  Set up ssh on Primary with our user](#Step-16-Set-up-ssh-on-Primary-with-our-user)
- [Step 17.  Copy the ssh key our secondary machines](#Step-17-Copy-the-ssh-key-our-secondary-machines)
- [Step 18.  Configure Hadoop Service Port](#Step-18-Configure-Hadoop-Service-Port)
- [Step 19.  Configuration of HDFS system](#Step-19-Configuration-of-HDFS-system)
- [Step 20.  Identify the workers](#Step-20-Identify-the-workers)
- [Step 21.  Copy configurations into secondary machines](#Step-21-Copy-configurations-into-secondary-machines)
- [Step 22.  Formatting and Starting HDFS system](#Step-22-Formatting-and-Starting-HDFS-system)
- [Step 23.  Nodes management tool](#Step-23-Nodes-management-tool)
- [Step 24.  Yarn configuration](#Step-24-Yarn-configuration)
- [Step 25.  Start Yarn](#Step-25-Start-Yarn)
- [Step 26.  Set up Spark](#Step-26-Set-up-Spark)
- [Finish.](#Finish.)

## Step 1 VMware Workstation pro 16 Network Setting

    On VMware Workstation settings make sure that your Network adapter is set for Bridged.

   ![hadoop-network-image](https://user-images.githubusercontent.com/39446946/104556503-0f294700-5683-11eb-95b7-977297bf6c59.PNG)

## Step 2 Install ssh

    Install ssh with the following command:

   ![image](https://user-images.githubusercontent.com/39446946/104557353-74ca0300-5684-11eb-9642-d44397f6f264.png)

## Step 3 Install pdsh

    Install psdh with the following command:

   ![image](https://user-images.githubusercontent.com/39446946/104557549-c4a8ca00-5684-11eb-9c15-d6be2fbc5096.png)

## Step 4 Set pdsh environment to ssh

    Open the Bashrc file with nano:

   ![image](https://user-images.githubusercontent.com/39446946/104558349-02f2b900-5686-11eb-9d94-c04ca4e2c502.png)

    Add to the end of the file:

   ![image](https://user-images.githubusercontent.com/39446946/104558405-156cf280-5686-11eb-83c1-8242df50eca0.png)

   ![image](https://user-images.githubusercontent.com/39446946/104558669-81e7f180-5686-11eb-941a-9d0a8567c4fb.png)

## Step 5 Generate a SSH key

    Generate a ssh key with the following command:

   ![image](https://user-images.githubusercontent.com/39446946/104558775-b196f980-5686-11eb-8549-5ab39a917230.png)

    Press Enter when asked to choose the storage file.

   ![image](https://user-images.githubusercontent.com/39446946/104558965-076ba180-5687-11eb-8a99-cb2bbe903ecb.png)

## Step 6 Clone the key into authorized_keys files

    To give the right permissions to your ssh key you should create a copy on authorized_keys files:

   ![image](https://user-images.githubusercontent.com/39446946/104559062-2c601480-5687-11eb-9ea3-7021774a9759.png)

   ![image](https://user-images.githubusercontent.com/39446946/104559477-caec7580-5687-11eb-8690-3cfad0bd7d98.png)

    Make sure that everything is well set, doing a ssh to our machine.

   ![image](https://user-images.githubusercontent.com/39446946/104559344-97115000-5687-11eb-89c2-2f19502167bb.png)

   ![image](https://user-images.githubusercontent.com/39446946/104559609-f8392380-5687-11eb-9ed5-a8ff2b55f811.png)

    * Your output may be different

## Step 7 Install Java 8

    In order to run Hadoop you need to have Java 8 install on your machine. To do so, use the follow command:

    (※Github: https://github.com/frekele/oracle-java/releases), Java-Version: "jdk-8u212-linux-x64.tar.gz"

    Download the "wget https://github.com/frekele/oracle-java/releases/download/8u212-b10/jdk-8u212-linux-x64.tar.gz" file.

    Unzip the "tar -xvzf jdk-8u212-linux-x64.tar.gz" file.

    Enter 'sudo nano /etc/profile' to set the Java path.

    sudo mv jdk1.8.0_212 /usr/local

   ![image](https://user-images.githubusercontent.com/39446946/104560943-f8d2b980-5689-11eb-82a9-e01a69a4d7e5.png)

    Check if Java it’s install with the following command:

   ![image](https://user-images.githubusercontent.com/39446946/104561124-3b949180-568a-11eb-923f-5c0fba90a08d.png)

## Step 8 It’s time to download and install Hadoop

    First download the tar file that contains Hadoop with the following command:

    "sudo wget -P ~ https://mirrors.sonic.net/apache/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz"

    When the download is finish unzip it:

   ![image](https://user-images.githubusercontent.com/39446946/104561562-edcc5900-568a-11eb-9691-f06463f3c0b8.png)

    And move it to a folder that will be called hadoop (it’s a practical solution, do not change the mechanics of the rest):

   ![image](https://user-images.githubusercontent.com/39446946/104561996-16ece980-568b-11eb-871b-ec11312745b5.png)

## Step 9 Set up Hadoop

    Start to configure the Java path on Hadoop’s virtual environment:

   ![image](https://user-images.githubusercontent.com/39446946/104561729-0472b000-568b-11eb-84f2-d71783721959.png)

    Then look for Java_Home’s line and replace it by:

   ![image](https://user-images.githubusercontent.com/39446946/104562048-29ffb980-568b-11eb-8363-d4121890c323.png)

## Step 10 Move the hadoop directory to our user local file

    Move it with the following command:

   ![image](https://user-images.githubusercontent.com/39446946/104562104-3b48c600-568b-11eb-9b6c-e883812bb70b.png)

## Step 11 Set up hadoop path

    To set up hadoop path on machine’s environment, open the environment file with:

   ![image](https://user-images.githubusercontent.com/39446946/104562197-63d0c000-568b-11eb-830c-6d54987331cf.png)

    PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/hadoop/bin:/usr/local/hadoop/sbin"
    JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"

   ![image](https://user-images.githubusercontent.com/39446946/104562301-8236bb80-568b-11eb-946f-4b8c78ad695a.png)

## Step 12 Create a specific user for Hadoop

    Start by creating a new user: (I choose to call it h-user, but feel free to choose other name)

   ![image](https://user-images.githubusercontent.com/39446946/104562551-db9eea80-568b-11eb-8233-5cd21b1138fc.png)

    Now you need to give this user permissions to work within hadoop’s folder.

   ![image](https://user-images.githubusercontent.com/39446946/104562605-eeb1ba80-568b-11eb-9cf8-457171ca7b8a.png)

## Step 13 Clone the primary machine in order to create two secondary machines

    Make three full clones of the primary machine:

   ![image](https://user-images.githubusercontent.com/39446946/104562720-0db04c80-568c-11eb-96ec-2074937adb29.png)

## Step 14 Change hostnames

    Start for changing the hostnames: (computer’s name)

   ![image](https://user-images.githubusercontent.com/39446946/104562879-45b78f80-568c-11eb-9f70-3f88f1aa6901.png)

   ![image](https://user-images.githubusercontent.com/39446946/104563050-857e7700-568c-11eb-8b65-74726eb9bc65.png)

    Do the same for secondary machines:

   ![image](https://user-images.githubusercontent.com/39446946/104563244-c080aa80-568c-11eb-91ad-8cc1984c6682.png)

   ![image](https://user-images.githubusercontent.com/39446946/104564980-f030b200-568e-11eb-8df5-b2636b8edc08.png)

   ![image](https://user-images.githubusercontent.com/39446946/104563415-f6be2a00-568c-11eb-9fa1-630d94ad9ed8.png)

    Now reboot all machines.

## Step 15 Identify machine’s ip

    To know the machine’s IP use:

   ![image](https://user-images.githubusercontent.com/39446946/104563497-11909e80-568d-11eb-9a6f-6975cc345a51.png)

    Write down all the IP’s.

    Now change the hosts file on all machines:

   ![image](https://user-images.githubusercontent.com/39446946/104563607-338a2100-568d-11eb-935f-37a7a33cdeed.png)

   ![image](https://user-images.githubusercontent.com/39446946/104563999-b9a66780-568d-11eb-8b20-6b8d4afc6329.png)

## Step 16 Set up ssh on Primary with our user

    Start for changing user:

   ![image](https://user-images.githubusercontent.com/39446946/104564181-f07c7d80-568d-11eb-8b8d-3ae29316e118.png)

    Now you need to generate a ssh key for this user:

   ![image](https://user-images.githubusercontent.com/39446946/104564229-01c58a00-568e-11eb-978c-c868fa58f449.png)

## Step 17 Copy the ssh key our secondary machines

    Copy the already generated key to all the machines:

    * "ssh-copy-id hadoop-user@hadoop-master"

    * "ssh-copy-id hadoop-user@hadoop-slave1"

    * "ssh-copy-id hadoop-user@hadoop-slave2"

    * "ssh-copy-id hadoop-user@hadoop-slave3"

## Step 18 Configure Hadoop Service Port

    Change hadoop port configurations: (only on primary)

   ![image](https://user-images.githubusercontent.com/39446946/104564455-43eecb80-568e-11eb-953d-3c469c23d77b.png)

    And then add to file’s configuration:

   ![image](https://user-images.githubusercontent.com/39446946/104564503-536e1480-568e-11eb-9e25-3fba3e64b1b2.png)

## Step 19 Configuration of HDFS system

    Change HDFS configurations: (only on primary)

   ![image](https://user-images.githubusercontent.com/39446946/104564559-65e84e00-568e-11eb-886b-b578625a1134.png)

    And then add to file’s configuration:

   ![image](https://user-images.githubusercontent.com/39446946/104564597-74cf0080-568e-11eb-889e-c0f98ae9c3fc.png)

## Step 20 Identify the workers

    Add the secondary machines to workers file: (only on primary)

   ![image](https://user-images.githubusercontent.com/39446946/104564634-831d1c80-568e-11eb-8b04-37040cc7f1a9.png)

   ![image](https://user-images.githubusercontent.com/39446946/104564722-9af4a080-568e-11eb-8214-44c0c98d400a.png)

## Step 21 Copy configurations into secondary machines

    You need to make sure that all the configurations that you just change are going to all machines, to do so, execute the following commands:

    * hadoop-slave1: scp /usr/local/hadoop/etc/hadoop/* hadoop-slave1:/usr/local/hadoop/etc/hadoop/

    * hadoop-slave2: scp /usr/local/hadoop/etc/hadoop/* hadoop-slave2:/usr/local/hadoop/etc/hadoop/

    * hadoop-slave3: scp /usr/local/hadoop/etc/hadoop/* hadoop-slave3:/usr/local/hadoop/etc/hadoop/

## Step 22 Formatting and Starting HDFS system

    Start for making sure that all changes are applied:

   ![image](https://user-images.githubusercontent.com/39446946/104565094-1ce4c980-568f-11eb-9c1d-5af0d6401fd6.png)

    Then format the hdfs system with:

   ![image](https://user-images.githubusercontent.com/39446946/104565128-29692200-568f-11eb-9304-9c4baa192c11.png)

    Make sure that your .bashrc file is configure:

   ![image](https://user-images.githubusercontent.com/39446946/104573051-cd56cb80-5697-11eb-81df-9d59adaf827c.png)

    And check if in the end of the file have the following path:

   ![image](https://user-images.githubusercontent.com/39446946/104573123-e2cbf580-5697-11eb-87bb-21830b891d5d.png)

    Update the changes:

   ![image](https://user-images.githubusercontent.com/39446946/104573162-eeb7b780-5697-11eb-84e9-131d12a849d5.png)

    When this operations are done, start the service:

   ![image](https://user-images.githubusercontent.com/39446946/104573200-f9724c80-5697-11eb-9dad-5a787a325261.png)

    To check if all the machines are using the correct resources use:

   ![image](https://user-images.githubusercontent.com/39446946/104573249-04c57800-5698-11eb-921b-5a4e1395433c.png)

    * Output hadoop-master:

   ![image](https://user-images.githubusercontent.com/39446946/104604665-ed4eb500-56c0-11eb-90b2-006bd7d70275.png)

    * Output hadoop-slave1:

   ![image](https://user-images.githubusercontent.com/39446946/104604769-0eafa100-56c1-11eb-842c-ccbb8e08a9dd.png)

    * Output hadoop-slave2:

   ![image](https://user-images.githubusercontent.com/39446946/104604830-1ff8ad80-56c1-11eb-910f-051bfc946a88.png)

    * Output hadoop-slave3:

   ![image](https://user-images.githubusercontent.com/39446946/104604882-2d159c80-56c1-11eb-96b0-161544e0b361.png)

## Step 23 Nodes management tool

   It’s time to check if all is working fine. Write primary’s IP on your browser using port 9870. 

   ![image](https://user-images.githubusercontent.com/39446946/104608579-64864800-56c5-11eb-9e39-0ac66ff1aca6.png)

   ![image](https://user-images.githubusercontent.com/39446946/104608884-c6df4880-56c5-11eb-8465-5d8573d084bf.png)

## Step 24 Yarn configuration

    To set up yarn you need to start for exporting all paths: (on hadoop-master)

   ![image](https://user-images.githubusercontent.com/39446946/104610076-0f4b3600-56c7-11eb-9329-aa756c620ce4.png)

    Now just change yarn’s configuration on both secondarys:

   ![image](https://user-images.githubusercontent.com/39446946/104610155-22f69c80-56c7-11eb-8081-b6c2d0e8a0ab.png)

    And then add the following configurations: (On hadoop-slave1, hadoop-slave2, hadoop-slave3)

   ![image](https://user-images.githubusercontent.com/39446946/104610207-30ac2200-56c7-11eb-8f84-76d438e39957.png)

## Step 25 Start Yarn 

    To start the Yarn service use: (On hadoop-master)

   ![image](https://user-images.githubusercontent.com/39446946/104610312-51747780-56c7-11eb-91b0-d838403ddda6.png)

    To have acess to Yarn’s management tool use your browser to acess to primary IP on port 8088:

   ![image](https://user-images.githubusercontent.com/39446946/104610447-7c5ecb80-56c7-11eb-9c93-117dcb52cf5b.png)

    As you can see, the cluster shows 3 active nodes!

## Step 26 Set up Spark

    Installing and Setting up a Yarn-Based Spark
        $ wget https://dlcdn.apache.org/spark/spark-3.1.3/spark-3.1.3-bin-hadoop3.2.tgz
        $ tar -xvf spark-3.1.3-bin-hadoop3.2.tgz
        $ mv spark-3.1.3-bin-hadoop3.2 spark
        
    Modify bashrc file
        export SPARK_HOME=/home/lect/spark
        export PYTHONPATH=$SPARK_HOME/python/lib/pyspark.zip:$SPARK_HOME/python/lib/py4j-0.10.9-src.zip
        export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
        export YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop
        export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
        export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH
        
    Reflect Changes
        $ source ~/.bashrc

    Creating and modifying the spark-defaults.conf file 
        spark.master                     yarn
        spark.eventLog.enabled           true
        spark.eventLog.dir               file:///home/dblab/spark/sparkeventlog
        spark.serializer                 org.apache.spark.serializer.KryoSerializer
        spark.driver.memory              40g
        spark.yarn.am.memory             4g
        spark.executor.instances         20
        spark.executor.cores             4
        spark.executor.memory            7g

    Running the Spark Master
        $ ~/spark/sbin$./start-master.sh
 
    Running the Spark workers
        $ ~/spark/sbin$./start-workers.sh 
        
## Finish.

