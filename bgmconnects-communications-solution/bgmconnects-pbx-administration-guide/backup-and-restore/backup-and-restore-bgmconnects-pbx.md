# Backup and Restore BGMconnects PBX

This article provides procedures for backing up and restoring a PBX server. The procedures are designed to ensure no data loss in upgrading and migration.

Backup files and data should be stored on a different server than the one that is used for daily running.

All procedures are performed at the command prompt and require root-level access.

## **Creating a Backup Using Snapshots**

If your PBX is running within a virtual environment or hosted on a cloud platform, it’s likely that these platforms offer the capability to create a snapshot of the server. This is a highly recommended method for backing up your current PBX server.

## **Restoring from a Snapshot**

Restoring your PBX from a snapshot is a straightforward process. Simply follow the steps provided by your virtual environment or cloud platform to restore the PBX from the snapshot you’ve created.

Remember, it’s always a good idea to test the restore process periodically to ensure your backups are working as expected. This will help you avoid any surprises in the event of a system failure.

## **Backing Up PBX Data**

### **Linux**

When [installing BGMconnects on Linux](/broken/pages/yGaVQdkFEavISR5V0QGV), in step 3, you typically use the following command to create the BGMconnects Docker instance as below:

**v22.x:**

```sh
sudo /bin/sh pbx_ctl.sh \
run -p /var/lib/bgmconnects \
-a 66.175.221.120 \
-i bgmconnects/pbx:22
```

**v16.x:**

```shell
/bin/sh pbx_ctl.sh \
run -p /var/lib/bgmconnects \
-a 66.175.221.120 \
-i bgmconnects/pbx:16
```

In the above command used to create the BGMconnects Docker instance, the `-p` parameter is used to specify the **parent** folder for storing the PBX data. To back up the data, simply copy the folder `/var/lib/bgmconnects/pbx` and `/var/lib/bgmconnects/postgresql` to another server or an external disk.

Now back up the data.

**v22.x:**

<pre class="language-bash"><code class="lang-bash"><strong>sudo mkdir -p /back/pbx-data
</strong><strong>sudo cp -p -r /var/lib/bgmconnects/pbx /back/pbx-data
</strong><strong>sudo mkdir -p /back/pbx-db
</strong>sudo cp -p -r /var/lib/bgmconnects/postgresql /back/pbx-db
</code></pre>

For example, if you specified the **parent** path as `/bgmconnects/data` using the `-p` parameter when installing the PBX, then you need to back up the folder `/bgmconnects/data/pbx` and `/bgmconnects/data/postgresql`.

```sh
sudo mkdir -p /back/pbx-data
sudo cp -p -r /bgmconnects/data/pbx /back/pbx-data
sudo mkdir -p /back/pbx-db
sudo cp -p -r /bgmconnects/data/postgresql /back/pbx-db
```

**v16.x:**

```sh
mkdir -p /back/pbx-data
cp -p -r /var/lib/bgmconnects/pbx /back/pbx-data
mkdir -p /back/pbx-db
cp -p -r /var/lib/bgmconnects/postgresql /back/pbx-db
```

For example, if you specified the **parent** path as `/bgmconnects/data` using the `-p` parameter when installing the PBX, then you need to back up the folder `/bgmconnects/data/pbx` and `/bgmconnects/data/postgresql`.

```sh
mkdir -p /back/pbx-data
cp -p -r /bgmconnects/data/pbx /back/pbx-data
mkdir -p /back/pbx-db
cp -p -r /bgmconnects/data/postgresql /back/pbx-db
```

After successfully backing up the data, save it safely.

### **Windows**

When [installing BGMconnects on Windows](/broken/pages/OR9aunjWJKcIQshxSgNh), in step 1, there is an option that allows you to choose the **parent** folder for storing the PBX data.

To back up the data, copy this folder to another server or an external disk. By default, if you didn’t specify otherwise, the **parent** folder is `C:\ProgramData\BGMconnects`.

The following folders need to be copied:

* C:\ProgramData\BGMconnects\pbx
* C:\ProgramData\BGMconnects\postgresql
* C:\ProgramData\BGMconnects\html

## **Restoring from Backup Data on Linux for PBX v22.x**

Please follow the steps below to restore the PBX from the backup data in a Linux environment.

{% hint style="danger" %}
You can't restore the backup data of a Windows PBX to a Linux PBX.
{% endhint %}

### **Restoring from Backup Data to the Same Server**

1. Stop the current PBX and delete the PBX data.

```sh
cd /opt/bgmconnects && sudo /bin/sh pbx_ctl.sh stop
```

```sh
sudo /bin/sh pbx_ctl.sh rm
```

<pre class="language-sh"><code class="lang-sh"><strong>sudo rm -rf /var/lib/bgmconnects/pbx/*
</strong></code></pre>

```sh
sudo rm -rf /var/lib/bgmconnects/postgresql/*
```

2\. Restoring the PBX

First, copy the backup data to the BGMconnects server. You can use the default folder, such as `/var/lib/bgmconnects`, or another folder of your choice.

For example:

<pre class="language-sh"><code class="lang-sh"><strong>sudo mkdir -p /var/lib/bgmconnects/pbx
</strong><strong>sudo cp -p -r /back/pbx-data/pbx /var/lib/bgmconnects/
</strong><strong>sudo mkdir -p /var/lib/bgmconnects/postgresql
</strong>sudo cp -p -r /back/pbx-db/postgresql /var/lib/bgmconnects/
</code></pre>

{% hint style="danger" %}
After copying the data, make sure that the folder, all subfolders, and files have the correct permissions set to `888:888`.
{% endhint %}

The command below is used to create and run the PBX on a server with the IP `66.175.221.120`. If you’re running the PBX in a LAN without a public IP, replace `66.175.221.120` with the PBX server’s private LAN IP. If you copied the backup data to a folder other than `/var/lib/bgmconnects`, make sure to use the actual folder with parameter **-p** in the commands below.

```bash
sudo /bin/sh pbx_ctl.sh \
run -p /var/lib/bgmconnects \
-a 66.175.221.120 \
-i bgmconnects/pbx:22
```

Congratulations! Your PBX has now been successfully restored.

### **Restoring Backup Data to a New PBX Server**

If you want to restore the backup PBX v22.x data to another new server, please follow the below steps.

**Note**, that once you successfully restore the PBX data to the new server, the PBX will be upgraded to the latest v22.x automatically.

1. prepare the new Linux server, **don't** install the PBX.

Copy the backup data to the new server. You can use the default folder, such as `/var/lib/bgmconnects`, or another folder of your choice.

<pre class="language-sh"><code class="lang-sh"><strong>sudo mkdir -p /var/lib/bgmconnects/pbx
</strong><strong>sudo cp -p -r /back/pbx-data/pbx /var/lib/bgmconnects/
</strong><strong>sudo mkdir -p /var/lib/bgmconnects/postgresql
</strong>sudo cp -p -r /back/pbx-db/postgresql /var/lib/bgmconnects/
</code></pre>

{% hint style="danger" %}
After copying the data, make sure that the folder, all subfolders, and files have the correct permissions set to `888:888`.
{% endhint %}

2. Now follow the guide [Install BGMconnects on Linux](/broken/pages/yGaVQdkFEavISR5V0QGV) to install a new PBX with your restored PBX data by using the **-p** parameter to specify the restored data path.

After successfully installing the PBX, your restored PBX data now is attached to the newly installed PBX.

After signing into the PBX web portal, launch the BGMconnects Setup Wizard. In step 1 of the Setup Wizard, make sure to update the PBX IP address to match the new server’s IP.

## **Restoring from Backup Data on Linux for PBX v16.x**

Please follow the steps below to restore the PBX from the backup data in a Linux environment.

{% hint style="danger" %}
You can't restore the backup data of a Windows PBX to a Linux PBX.
{% endhint %}

### **Restoring from Backup Data to the Same Server**

1. Stop the current PBX and delete the PBX data.

```sh
cd /opt/bgmconnects && /bin/sh pbx_ctl.sh stop
```

```sh
/bin/sh pbx_ctl.sh rm
```

<pre class="language-sh"><code class="lang-sh"><strong>rm -rf /var/lib/bgmconnects/pbx/*
</strong></code></pre>

```sh
rm -rf /var/lib/bgmconnects/postgresql/*
```

2\. Restoring the PBX

First, copy the backup data to the PBX server. You can use the default folder, such as `/var/lib/bgmconnects`, or another folder of your choice.

For example:

<pre class="language-sh"><code class="lang-sh"><strong>mkdir -p /var/lib/bgmconnects/pbx
</strong><strong>cp -p -r /back/pbx-data/pbx /var/lib/bgmconnects/
</strong><strong>mkdir -p /var/lib/bgmconnects/postgresql
</strong>cp -p -r /back/pbx-db/postgresql /var/lib/bgmconnects/
</code></pre>

{% hint style="danger" %}
After copying the data, make sure that the folder, all subfolders, and files have the correct permissions set to `888:888`.
{% endhint %}

The command below is used to create and run the PBX on a server with the IP `66.175.221.120`. If you’re running the PBX in a LAN without a public IP, replace `66.175.221.120` with the PBX server’s private LAN IP. If you copied the backup data to a folder other than `/var/lib/bgmconnects`, make sure to use the actual folder with parameter **-p** in the commands below.

```bash
/bin/sh pbx_ctl.sh \
run -p /var/lib/bgmconnects \
-a 66.175.221.120 \
-i bgmconnects/pbx:16
```

Congratulations! Your PBX has now been successfully restored.

### **Restoring Backup Data to a New PBX Server**

If you want to restore the backup PBX v16.x data to another new server, please follow the below steps.

**Note**, that once you successfully restore the PBX data to the new server, the PBX will be upgraded to the latest v16.x automatically.

1. prepare the new Linux server, **don't** install the PBX.

Copy the backup data to the new server. You can use the default folder, such as `/var/lib/bgmconnects`, or another folder of your choice.

<pre class="language-sh"><code class="lang-sh"><strong>mkdir -p /var/lib/bgmconnects/pbx
</strong><strong>cp -p -r /back/pbx-data/pbx /var/lib/bgmconnects/
</strong><strong>mkdir -p /var/lib/bgmconnects/postgresql
</strong>cp -p -r /back/pbx-db/postgresql /var/lib/bgmconnects/
</code></pre>

{% hint style="danger" %}
After copying the data, make sure that the folder, all subfolders, and files have the correct permissions set to `888:888`.
{% endhint %}

2. Now follow the guide [Installation of BGMconnects v16.x](/broken/pages/WDkBBp3AwjOAXnEaatRd) to install a new PBX with your restored PBX data by using the **-p** parameter to specify the restored data path.

After successfully installing the PBX, your restored PBX data now is attached to the newly installed PBX.

After signing into the PBX web portal, launch the PBX Setup Wizard. In step 1 of the Setup Wizard, make sure to update the PBX IP address to match the new server’s IP.

## **Restoring from Backup Data on Windows**

Please follow the steps below to restore the PBX from the backup data in a Windows environment.

{% hint style="danger" %}
You can't restore the backup data of a Linux PBX to a Windows PBX.
{% endhint %}

### **1. Uninstall the Currently Running PBX Instance**

* Uninstall the PBX from Windows
* Delete the below PBX data folders:
  * C:\ProgramData\BGMconnects\pbx
  * C:\ProgramData\BGMconnects\postgresql
  * C:\ProgramData\BGMconnects\html
  * C:\Program Files\BGMconnects\PBX

### **2. Upgrading the BGMconnects Installer (Optional)**

You have the option to upgrade the BGMconnects Installer before restoring the PBX data. The latest BGMconnects installer for Windows can be downloaded from the [BGMconnects website](https://www.bgmconnects.com/downloads/).

### **3. Restoring the PBX**

First, copy the backup data to the PBX server folders:

* C:\ProgramData\BGMconnects\pbx
* C:\ProgramData\BGMconnects\postgresql
* C:\ProgramData\BGMconnects\html

You can use the default folder as the data **parent** folder, such as `C:\ProgramData\BGMconnects`, or another folder of your choice.

Next, double-click the BGMconnects installer to install the PBX. In the installation UI, choose the PBX data **parent** folder ( `C:\ProgramData\BGMconnects`), then click the `Next` button. Wait for the installation to complete.

Congratulations! Your PBX has now been successfully restored.

#### **Restoring Backup Data to a New PBX Server**

The steps for restoring backup data to a new PBX server are essentially the same.

After signing into the PBX web portal, launch the BGMconnects Setup Wizard. In step 1 of the Setup Wizard, make sure to update the PBX IP address to match the new server’s IP.
