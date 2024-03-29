# Self-fixed Technical Debt
# About

This is a repository for the paper 

**Does it matter who pays back Technical Debt? An empirical study of self-fixed TD**

It contains the replication package of the study reported in the aforementioned paper.

# Replication Instructions

Most of the workload to replicate this project is automated through scripts. 

To reduce the effort further, we also automated the creation of an environment for the study.

The instruction to create the environment and replicate the study are described in the following. 

## 1. Bootstrap Virtual Machine

### Requirements

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)
3. Install the plugin `vagrant-docker-compose`. In your command prompt or terminal, run:
```shell
$ vagrant plugin install vagrant-docker-compose 
```
4. (Optional) Install the plugin `vagrant-vbguest` (VirtualBox Guest Additions). In your command prompt or terminal, run:
```shell
$ vagrant plugin install vagrant-vbguest 
```

### Using the Virtual Machine (VM)

The VM is controlled via [Vagrant](https://www.vagrantup.com/downloads.html) and contains the configured environment to run all scripts for this study. Mainly, the VM provides:
- SonarQube (version 7.6-community)
- PostgreSQL (version 11, to store SonarQube data)
- Jupyter + Python/Java + libraries (to run scripts)

Whenever you boot the VM, the environment is initialized and SonarQube is available at http://localhost:9000.

You can control the VM via a command prompt (Windows) or terminal (Linux + MacOS). For that, you:
1. Open a command prompt or terminal
2. On it, navigate to the root folder of this repository
3. Execute one of the following commands

There are several commands available, but we focus on the ones necessary for the study.

```bash
# Boot the VM
$ vagrant up
```

```bash
# Stop the VM
$ vagrant halt
```

```bash
# Purge the VM
$ vagrant destroy
```

```bash
# Connect (via SSH) to the VM
$ vagrant ssh
```

> **Important Notes** 
>
> The first boot (or the boot after purging) takes a long time, as it will:
> * download and configure the VM
> * download and configure the tools (e.g., SonarQube)
>
> The next boots are much quicker as you just "turn the machine on"
> 
> Purging the VM will delete all VM files except for the ones in this folder (and subfolders).


## 2. Additional SonarQube Configurations

Before you run the scripts for the study, you have to configure SonarQube as follows:

1. Change the General Settings in the following way:
    * Administration -> Configuration -> General (set each value instead of default value):
    - Keep only one analysis a day after -> 876000
    - Keep only one analysis a week after -> 5200
    - Keep only one analysis a month after -> 5200
    - Keep only analyses with a version event after -> 10400
    - Delete all analyses after -> 10400
    - Delete closed issues after -> 36500

2. Activate more Python/Java rules:

    * Quality Profiles -> Python/Java -> Sonar way, from the drop-down menu click on Copy and set a name
    * Then click on Inactive and then Bulk Change -> Activate In...
    * Back to  Quality Profiles and set the new profile as Default (from the drop-down)
    
## 3. Data Collection

To collect the data for the study, you must follow the instructions described in the Jupyter notebook at `study.d/Data-Collection.ipynb`. For that:

1. Open [Jupyter Lab](http://localhost:8888/lab) on your browser (*password: sonar*)

2. There is a file tree on the left, click on `Data-Collection.ipynb`

## 4. Content

The following table describes the content of each file for each RQ in this package.

- `RQ1.R`\
  R script to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and several project characteristics: the number of commits, number of developers, SLOC, and the total number of issues. 

- `RQ1.csv`\
  The dataset used to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and several project characteristics: the number of commits, number of developers, SLOC, and the total number of issues.

- `RQ2.R`\
  R script to conduct Wilcoxon Rank Sum tests, Cliff's Delta Effect Size and the Scott-Knott ESD test. 

- `RQ2_ScottKnott.csv`\
  The dataset used to conduct the Scott-Knott ESD test, including the self-fixing rate of each rule.

- `RQ2_Wlcoxon.csv`\
  The dataset used to conduct Wilcoxon Rank Sum tests and Cliff's Delta Effect Size, including the self-fixing rate of each project for five types of TD. It is worth noting that there are some projects where no Test or Document Debt is detected.

- `RQ3_ScottKnott.R`\
  R script to conduct the Scott-Knott ESD test. 
  
- `RQ3_ScottKnott.csv`\
  The dataset used to conduct the Scott-Knott ESD test, including the percentages of issues that have been self-fixed within the three time-frames for all five debt types.
  
- `RQ3_SurvivalAnalysis.R`\
  R script to generate Figure.2: Results of Kaplan-Meier method for the survival time of self-fixed and non-self-fixed issues.  

- `RQ3_SurvivalAnalysis.csv`\
  The dataset used to generate Figure.2: Results of Kaplan-Meier method for the survival time of self-fixed and non-self-fixed issues. 

- `RQ4.R`\
  R script to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and two variables (i.e., the number of developers involved in a file and the number of changes that developers made to a file).

- `RQ4.csv`\
  The dataset used to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and two variables (i.e., the number of developers involved in a file and the number of changes that developers made to a file).
  
- `RQ5.R`\
  R script to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and four variables (i.e., developers' seniority, file count, commit count and commit size).

- `RQ5.csv`\
  The dataset used to build a generalized linear mixed model to investigate the relationship between the likelihood of an issue being self-fixed and two variables (i.e., developers' seniority, file count, commit count and commit size).

