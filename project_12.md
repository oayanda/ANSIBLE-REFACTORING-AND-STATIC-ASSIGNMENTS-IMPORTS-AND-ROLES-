# Step 1 – Jenkins House Cleaning

Create a directory in the Jenkins server to to reduce space and streamline for every build or code change that happens on the job.

Go to your Jenkins-Ansible server and create a new directory called `ansible-config-artifact` – we will store there all artifacts after each build.

```bash
sudo mkdir /home/ubuntu/ansible-config-artifact

#Change permissions to this directory, so Jenkins could save files there

sudo chmod -R 0777 /home/ubuntu/ansible-config-artifact
```

![create a directory](./images/1.png)
Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for `Copy Artifact` and install this plugin without restarting Jenkins

![create a directory](./images/2.png)

Now create a `new Freestyle` project job called `save_artifacts`.

Configure the project to be triggered by completion of your existing ansible project `Ansible`. Configure it accordingly:

![create a directory](./images/3.png)

>The number of builds kept is varies according to your needs.

The main idea of `save_artifacts` project is to save artifacts into `/home/ubuntu/ansible-config-artifact` directory. To achieve this, create a `Build step` and choose `Copy artifacts from other project`, specify ansible as a source project and `/home/ubuntu/ansible-config-artifact` as a target directory. Apply and save configuration.

![create a directory](./images/4.png)

Test your set up by making some change in `README.MD` file inside your `ansible-config-mgt` repository

![create a directory](./images/5.png)

The Jenkins Job completed successfully. Now the Jenkins pipeline is more neat and clean.

![create a directory](./images/6.png)

## REFACTOR ANSIBLE CODE BY IMPORTING OTHER PLAYBOOKS INTO SITE.YML

Let's Refactor Ansible code by importing other playbooks into site.yml

> Create a new branch to work from called `refactor`
![create a directory](./images/7.png)

Within playbooks folder, create a new file and name it `site.yml` – This file will now be considered as an entry point into the entire infrastructure configuration. Other playbooks will be included here as a reference. In other words, `site.yml` will become a parent to all other playbooks that will b
![create a directory](./images/8.png)
