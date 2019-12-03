![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 如何使用AlwaysOn将SQL 2012升级到SQL 2014
#### How To Upgrade SQL 2012 to SQL 2014 With AlwaysOn
**发布-日期: 2016年7月20日 (评论)**

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
在AlwaysOn配置开始从SQL 2012升级到SQL 2014之前，需要确定一些事项。在这个例子中，我们将主要使用默认配置。另外，如果你安装了Reporting Services但尚未配置，我们将看到一个简单但最常见的错误。它通常会抛出错误消息，但最简单的解决方法是为ReportServer和ReportServerTempDB配置Reporting Services数据库（再次使用默认值）。我们还将介绍在将AlwaysOn配置升级到SQL Server 2014时经常遇到的一些特殊同步错误。
注意：这不是向你展示所有的“如何操作”，这只是为你提供了一些预期的参考，并不全面。它向你展示了可能出现的各种问题，可以快速解决问题的方法，但它不会在升级过程中“训练”你。
对于初学者，确保使用“rolling upgrade”过程执行升级，首先将SQL Server 2014安装到被动节点（或节点）上，然后将Availability Group资源（和其他资源）故障转移到辅助节点，然后执行前主节点。
确保你的AlwaysOn方案处于Synchonous模式（主节点保持所有权）。
每当你准备好做最后执行时，你需要将可用性资源组移动到已升级的辅助服务器。

步骤1：

一旦软件下载完成，则需要安装它。只需右键单击并选择“Mount”即可。

## English
Here’s a couple things you need to make sure of before you begin the upgrade from SQL 2012 to SQL 2014 within an AlwaysOn configuration. In this example we’ll be using mostly the default configurations. Additionally; we’ll see a single (most commonly found error) if you have Reporting Services installed, but not yet configured. It will usually throw an error message, but the easiest fix is to configure the Reporting Services Databases ( again using the defaults ) for ReportServer, and ReportServerTempDB. We’ll also cover some peculiar synchronization errors that are often encountered whenever upgrading an AlwaysOn configuration to SQL Server 2014.
Note: This is not the ‘How to’ that shows you everything. This simply gives you a reference on some of the things to expect. This is NOT comprehensive. It shows you various issues that might crop up, quick ways to potentially resolve them, but it will not ‘train’ you on the upgrade process.
For starters; ensure that you are performing the upgrade using the ‘rolling upgrade’ process where you are installing SQL Server 2014 onto the passive node (or nodes) first, then failing over the Availability Group resource ( And other resources to the secondary Node), then doing the former primary node last.
Ensure that your AlwaysOn scheme is in Synchonous Mode (where the primary node maintains ownership).
Whenever you’re ready to do the final server; you’ll need to move the availability resource group to the already upgraded secondary server.

Step 1:

Once you download the software you’ll need to mount it. Simply right-click and select ‘Mount’.



![#](images/01-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 2:
Right-click ‘Setup’ and select ‘Run as Administrator’.
步骤2:
右键单击“Setup”，然后选择“Run as Administrator”。

![#](images/02-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 3:
Select ‘Installation’, and choose ‘Upgrade from SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, or SQL Server 2012’.
步骤3:
选择“Installation”，然后选择“Upgrade from SQL Server 2005, SQL Server 2008, SQL Server 2008 R2, or SQL Server 2012”。

![#](images/03-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 4:
Enter your product Key and click ‘Next’. In this example I’ve removed the Product Key for obvious reasons.
步骤4:
输入你的产品密钥，然后单击“Next”。在这个例子中，我已经删除了产品密钥，原因很明显。

![#](images/04-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 5:
Accept the ‘License Terms’ and click ‘Next’.
步骤5:
接受“License Terms”并单击“Next”。

![#](images/05-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 6:
Click ‘Next’.
步骤6:
单击“Next”。

![#](images/06-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 7:
Click ‘Next’ at the ‘Install Setup Files’ screen.
步骤7:
单击“Install Setup Files”屏幕上的“Next”。

![#](images/07-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 8:
Use the default selection (In case upgrading the current server using a single default instance), and click ‘Next’.
步骤8:
使用默认选择（如果使用单个默认实例升级当前服务器），然后单击“Next”。

![#](images/08-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 9:
Click ‘Next’. The feature selection will default to all the current features that exist on the Database Server.
Note:
They are preselected. ( This is normal for the upgrade process )
They cannot be unselected or changed. Again… This is normal.
步骤9:
点击“Next”。功能选择项将默认为数据库服务器上存在的所有当前功能。
注意：
它们是预先选定的。（这对升级过程来说是正常的）
它们不能被取消选择或改变。再次强调一遍，这很正常。

![#](images/09-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 10:
Click ‘Next’ at the instance configuration. We are using the defaults in this example tutorial.
步骤10:
单击实例配置中的“Next”.我们在本示例教程中使用默认值。

![#](images/10-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 11:
Click ‘Next’.
步骤11:
单击“Next”。

![#](images/11-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 12:
步骤12:

![#](images/12-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 13:
步骤13:

![#](images/13-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 14:
步骤14:

![#](images/14-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Note the error boxes. If you get these they are easily corrected. Simply add a Reporting Services Database. If you don’t have this issue you won’t need to do the following step of creating one.
请注意错误框。如果你看到这些错误框，它们是很容易纠正的。只需添加Reporting Services数据库即可，如果你没有此问题，则无需执行以下创建操作。
Step 15:
步骤15:

![#](images/15-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 16:
步骤16:

![#](images/16-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 17:
步骤17:

![#](images/17-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 18:
步骤18:

![#](images/18-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 19:
步骤19:

![#](images/19-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 20:
步骤20:

![#](images/20-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
User name has been removed of course.
用户名已被删除。
Step 21:
步骤21:

![#](images/21-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 22:
步骤22:

![#](images/22-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Step 23:
步骤23:

![#](images/23-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Rerun the upgrade process and it should proceed to the next step where it will begin the installation. Be patient as this is the longest portion of the installation.
重新运行升级过程，并且下一步会继续开始安装。请耐心等待，因为这是安装中最长的部分。

![#](images/24-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Note: While the above progress bar completely fills… It will appear as though it’s maxed out and hung. Just relax; it’s not totally 100% done. Progress bar for this particular upgrade may not be totally accurate. It’s behind a couple minutes in some cases. It’s normal; just wait a few, then you’ll see the following screen.
注意：当上面的进度条显示完成，它看起来看起来好像是最大化，放轻松，它并非完全100％完成。此特定升级的进度条可能不完全准确，在某些情况下，它落后了几分钟，这是正常的，等一下，你会看到以下屏幕。

![#](images/25-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Next just follow-through with the remaining prompts however; there are a couple things you should keep in mind.
1. Run DBCC across all databases to ensure they are in a good working state.
2. Run a Backup of all databases.
3. (To keep it simple) Remove the Databases from the AlwaysOn configuration. Yes; this means you’ll need to add them back after the upgrade.
4. Failover the Availability Group, and other Cluster resources to the already upgraded Nodes before you do the last server.
Fyi; If you don’t remove the databases from the AlwaysOn configuration, and decide to run the upgrade on the primary node anyway (even after failing over the Cluster, and Availability group) you might get some peculiar errors. You’ll see this whenever you’re looking at the Failover Cluster Manager, or the AlwaysOn High Availability Dashboard after the upgrade.
接下来只是跟进剩下的提示，请记住几件事。
1.在所有数据库中运行DBCC以确保它们处于良好的工作状态。
2.运行所有数据库的备份。
3.（简单地）从AlwaysOn配置中删除数据库。没错，这意味着你需要在升级后添加它们。
4.在执行最后一个服务器之前，将Availability Group和其他Cluster资源故障转移到已升级的节点。
据说：如果不从AlwaysOn配置中删除数据库，并在主节点上运行升级（即使在故障转移Cluster和Availability group），你可能会遇到一些特殊错误。每当在升级后查看Failover Cluster Manager或AlwaysOn High Availability Dashboard时，你都会看到此信息。

![#](images/26-How-To-Upgrade-SQL-2012-to-SQL-2014-With-AlwaysOn.png?raw=true "#")
 
Just wanted to give you a heads-up on that one.
只想给你一个关于此问题的提示。



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

