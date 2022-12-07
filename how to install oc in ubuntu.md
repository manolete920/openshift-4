# Installing the OpenShift CLI on Windows

You can install the OpenShift CLI (`oc`) binary on Linux by using the following procedure.

Procedure

1. Navigate to the [OpenShift Container Platform downloads page](https://access.redhat.com/downloads/content/290) on the Red Hat Customer Portal.

2. Select the appropriate version in the **Version** drop-down menu.

3. Click **Download Now** next to the **OpenShift v4.6 Linux Client** entry and save the file.

4. Unpack the archive:

   

   ```
   $ tar xvzf <file>
   ```

5. Place the `oc` binary in a directory that is on your `PATH`.

   To check your `PATH`, execute the following command:

   

   ```
   $ echo $PATH
   ```

After you install the OpenShift CLI, it is available using the `oc` command:



```
$ oc <command>
```



Install Openshift OC Tool in Ubuntu 16.04
=========================================

### What is OC Tool?
OC tool stands for OpenShift Origin Client Tools

### Environment

* <b> Operating System</b> : Ubuntu 16.04 LTS (64-bit)

### Install OC tool in Ubuntu 16.04

The step by step installation guideline is shown below.

#### Download oc Client Tools
Download oc Client Tools for Linux from: [https://www.openshift.org/download.html](https://www.openshift.org/download.html)

#### Extract the downloaded `.tar.gz`
Extract the downloaded file and you will get `oc` file.

#### Move `oc` binary file to a directory in your local machine path
The `oc` file should be moved to any directory in the `path`. 
To check the `path` information of the local machine, open terminal and write:
```
echo $PATH
```
Now keep the `oc` file in any of these listed directory.

#### Apply Executable Permissions to the Binary
After keeping the `oc` file in any directory of the path you need to give execution permission to `oc` file.
Open terminal in the same path and do:
```
chmod +x SELECTED_PATH
```

#### Test the Installation
After successful installation of `oc` you can login to the console like below:
```
$ oc login
Server: 
Username: 
Password: 
Login successful.
Welcome! See 'oc help' to get started.
```

#### References

* OC download URL: [https://www.openshift.org/download.html](https://www.openshift.org/download.html)
* Getting started with CLI: [https://docs.openshift.org/latest/cli_reference/get_started_cli.html](https://docs.openshift.org/latest/cli_reference/get_started_cli.html)

https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html