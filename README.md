# Apache-Hadoop

Hadoop 3.2.1 Multi Node Cluster, Ubuntu 20.04

What is Hadoop?

“open-source software for reliable, scalable, distributed computing”, this means that is a framework for distributed processing.

It’s simply several computers working together in order to improve processing power and assure decentralize operations.

What do you need to start the set-up?

I will use Ubuntu Server 20.04. The recommended space on your computer would be 24GB.

# Step 1: VMware Workstation pro 16 Network Setting

On VMware Workstation settings make sure that your Network adapter is set for Bridged.

![hadoop-network-image](https://user-images.githubusercontent.com/39446946/104556503-0f294700-5683-11eb-95b7-977297bf6c59.PNG)

# Step 2: Install ssh

Install ssh with the following command:

![image](https://user-images.githubusercontent.com/39446946/104557353-74ca0300-5684-11eb-9642-d44397f6f264.png)

# Step 3: Install pdsh

Install psdh with the following command:

![image](https://user-images.githubusercontent.com/39446946/104557549-c4a8ca00-5684-11eb-9c15-d6be2fbc5096.png)

# Step 4: Set pdsh environment to ssh

Open the Bashrc file with nano:

![image](https://user-images.githubusercontent.com/39446946/104558349-02f2b900-5686-11eb-9d94-c04ca4e2c502.png)

Add to the end of the file:

![image](https://user-images.githubusercontent.com/39446946/104558405-156cf280-5686-11eb-83c1-8242df50eca0.png)

![image](https://user-images.githubusercontent.com/39446946/104558669-81e7f180-5686-11eb-941a-9d0a8567c4fb.png)

# Step 5: Generate a SSH key

Generate a ssh key with the following command:

![image](https://user-images.githubusercontent.com/39446946/104558775-b196f980-5686-11eb-8549-5ab39a917230.png)

Press Enter when asked to choose the storage file.

![image](https://user-images.githubusercontent.com/39446946/104558965-076ba180-5687-11eb-8a99-cb2bbe903ecb.png)

# Step 6: Clone the key into authorized_keys files

To give the right permissions to your ssh key you should create a copy on authorized_keys files:

![image](https://user-images.githubusercontent.com/39446946/104559062-2c601480-5687-11eb-9ea3-7021774a9759.png)

![image](https://user-images.githubusercontent.com/39446946/104559477-caec7580-5687-11eb-8690-3cfad0bd7d98.png)

Make sure that everything is well set, doing a ssh to our machine.

![image](https://user-images.githubusercontent.com/39446946/104559344-97115000-5687-11eb-89c2-2f19502167bb.png)

![image](https://user-images.githubusercontent.com/39446946/104559609-f8392380-5687-11eb-9ed5-a8ff2b55f811.png)

* Your output may be different

# Step 7: Install Java 8

In order to run Hadoop you need to have Java 8 install on your machine. To do so, use the follow command:

(※Github: https://github.com/frekele/oracle-java/releases), Java-Version: "jdk-8u212-linux-x64.tar.gz"

Download the "wget https://github.com/frekele/oracle-java/releases/download/8u212-b10/jdk-8u212-linux-x64.tar.gz" file.

Unzip the "tar-xvzf jdk-8u212-linux-x64.tar.gz" file.

Enter 'sudo nano /etc/profile' to set the Java path.

![image](https://user-images.githubusercontent.com/39446946/104560943-f8d2b980-5689-11eb-82a9-e01a69a4d7e5.png)

Check if Java it’s install with the following command:

![image](https://user-images.githubusercontent.com/39446946/104561124-3b949180-568a-11eb-923f-5c0fba90a08d.png)

# Step 8: It’s time to download and install Hadoop

First download the tar file that contains Hadoop with the following command:

"sudo wget -P ~ https://mirrors.sonic.net/apache/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz"

When the download is finish unzip it:

![image](https://user-images.githubusercontent.com/39446946/104561562-edcc5900-568a-11eb-9691-f06463f3c0b8.png)

And move it to a folder that will be called hadoop (it’s a practical solution, do not change the mechanics of the rest):

![image](https://user-images.githubusercontent.com/39446946/104561996-16ece980-568b-11eb-871b-ec11312745b5.png)

# Step 9: Set up Hadoop

Start to configure the Java path on Hadoop’s virtual environment:

![image](https://user-images.githubusercontent.com/39446946/104561729-0472b000-568b-11eb-84f2-d71783721959.png)

Then look for Java_Home’s line and replace it by:

![image](https://user-images.githubusercontent.com/39446946/104562048-29ffb980-568b-11eb-8363-d4121890c323.png)

# Step 10: Move the hadoop directory to our user local file

Move it with the following command:

![image](https://user-images.githubusercontent.com/39446946/104562104-3b48c600-568b-11eb-9b6c-e883812bb70b.png)

# Step 11: Set up hadoop path

To set up hadoop path on machine’s environment, open the environment file with:

![image](https://user-images.githubusercontent.com/39446946/104562197-63d0c000-568b-11eb-830c-6d54987331cf.png)

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/hadoop/bin:/usr/local/hadoop/sbin"
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"

![image](https://user-images.githubusercontent.com/39446946/104562301-8236bb80-568b-11eb-946f-4b8c78ad695a.png)

# Step 12: Create a specific user for Hadoop

Start by creating a new user: (I choose to call it h-user, but feel free to choose other name)

![image](https://user-images.githubusercontent.com/39446946/104562551-db9eea80-568b-11eb-8233-5cd21b1138fc.png)

Now you need to give this user permissions to work within hadoop’s folder.

![image](https://user-images.githubusercontent.com/39446946/104562605-eeb1ba80-568b-11eb-9cf8-457171ca7b8a.png)

# Step 13: Clone the primary machine in order to create two secondary machines

Make three full clones of the primary machine:

![image](https://user-images.githubusercontent.com/39446946/104562720-0db04c80-568c-11eb-96ec-2074937adb29.png)




