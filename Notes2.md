Configuring SQL security
Security is as important for an Azure SQL database installation as it is for on-premises servers. Once a database migration has been completed, administrators should confirm that the data¬bases in the cloud are protected, using tools such as the following:
■	Firewall rules Azure SQL Database supports two levels of firewall rules: server rules that specify the IP addresses permitted to access the server and database rules that control access to specific databases on the server.
■	Microsoft Defender for Azure SQL A comprehensive SQL security product that supports all of the Azure SQL products (at an additional cost). Administrators can apply Defender at the subscription level, to protect all of the SQL databases in the tenancy, or at the individual resource level.
■	SQL vulnerability assessment An Azure tool that uses Microsoft’s best practices knowledge base to examine a SQL installation for security issues, possibly caused by misconfigured parameters or permissions, and assess their severity.

Troubleshoot a migration
SQL data migrations to the Azure cloud are complicated efforts, often involving a variety of tasks and tools. Problems can occur at any point, typically generating error messages that administrators might not be able to act on while the migration is underway.
As noted earlier, when the Azure Data Migration Service is performing a migration, the DMS instance page in the Azure portal displays the current migration status in real time. In addition to the normal Restoring status, there are other status indicators that can indicate potential problems with the migration.
For example, a migration status of Running with errors indicates that DMS has encoun¬tered one or more errors, has retried them, and is continuing the migration. Administrators should check the migration logs afterward to determine the exact nature of the errors and whether any action is needed. A migration status of Failed indicates that the migration must be repeated once the administrator investigates the error and resolves the problem.
Other error message types that might appear during a SQL data migration include the following:
■	Version number errors Error messages that cite discrepancies between the version numbers of the source and target databases might require adjustments to compatibility level settings.
■	Database already exists Errors of this type indicate that a database with a duplicate name already exists on the target installation. The solution might just be a matter of specifying a different target database name.
■	Permission errors Errors citing denied permissions on the DMS account typically indicate that administrators must grant the specified permissions to the DMS service account.
 
Set up SQL Data Sync for Azure
SQL Data Sync is an Azure service that enables administrators to create bidirectional synchro¬nization relationships between SQL Database and SQL Server installations. The synchronization uses a hub-and-spoke topology in which two or more SQL databases are part of a sync group. One SQL database is designated as the hub database, while one or more others are member databases. Synchronization traffic occurs only between the hub and member databases. In addition to the databases participating in the sync group, there is also a sync metadata data¬base, which contains the metadata and logs for the Data Sync process.
Using SQL Data Sync, administrators can support hybrid applications by synchronizing an on-premises SQL Server database with an Azure SQL Database installation. Another possible application for Data Sync is to create synchronized copies of a database to split their opera¬tions: One copy can handle incoming queries while administrators use the other copy for data analytics.
To set up SQL Data Sync, an administrator opens an existing SQL Database installation in the Azure portal, chooses a database, and then selects Sync to other databases in the Data man¬agement menu. On the Sync to other databases page that appears, the administrator can then click +New sync group to open the Create Data Sync Group page, as shown in Figure 1-51.

FIGURE 1-51 The Create Data Sync Group page in the Azure portal

After creating the sync group, the administrator can add member databases to it. The data¬bases from other Azure SQL Database installations can be members of the sync group, as can
 
on-premises databases running on SQL Server. However, before a database from an
on-premises SQL Server can be a member of the sync group, administrators must first install the Azure SQL Data Sync Agent on the server. This agent connects to the hub database in the cloud, enabling the administrator to add the on-premises databases to the sync group as members.


Once the members are added to the sync group, administrators can select specific tables for synchronization on the sync group’s page. When the SQL Data Sync setup is completed, the administrator can manually trigger the synchronization from the sync group page or schedule it to occur at a specific time.

Implement a migration to Azure
As this chapter has shown, there are several tools that administrators can use to migrate
on-premises SQL databases to the Azure cloud. There are also several ways to launch and use those tools. When an Azure subscriber connects to the Azure portal, the Home page has a Create a resource icon that provides access to a long list of Azure services and Marketplace products.
On the Create a resource page, select the Migration category, as shown in Figure 1-52. This provides access to the Azure Data Migration Service and Azure Migrate tools covered earlier, as well as other tools that can aid in the migration process.

FIGURE 1-52 The Migration category in the Create a resource page in the Azure portal
 
Each icon includes links to the documentation for the tool, as well as a Create link that pro¬vides access to the tool itself, as follows:
■	Azure Database Migration Service Provides access to the Select migration scenario and Database Migration Service page, as described in “Implement an online migration strategy,” earlier in this chapter.
■	Azure Data Box Provides offline transfers of large amounts of data to or from Azure storage. Data Box Disk supports up to a 35 TB USB transfer, Data Box up to an 80 TB SMB or NFS transfer, and Data Box Heavy up to a 1 petabyte (PB) transfer in two separate nodes using SMB or NFS. The Create link opens the Get Started with Data Box page, as shown in Figure 1-53.
■	Azure Migrate Provides access to the Azure Migrate Get started page, as described in “Using Azure Migrate,” earlier in this chapter.
■	Azure Data Box Gateway A virtual appliance running on-premises that performs large online data transfers to or from Azure. The Create link opens the Create a Gateway resource page, on which the administrator specifies the Azure subscription, resource group, and region where the transferred data will be stored, and the instance name to be assigned to it.
■	Backup and Site Recovery The Azure Site Recovery service provides disaster recov-ery and failover services for Azure virtual machines. The Create link opens the Create Recovery Services vault page.

FIGURE 1-53 The Select your Azure Data Box page


Implement a migration between Azure SQL services
The most typical migration scenario is one in which an organization with on-premises SQL Server databases wants to migrate them to the Azure cloud, either as a hybrid solution or a
 
permanent one. However, there are also situations in which administrators want to migrate databases between Azure services. There are several ways to do that, depending on which services and how much data are involved.
Migrating a VM running SQL Server to a PaaS installation
From a migration standpoint, an Azure virtual machine running SQL Server is no different from an on-premises SQL Server installation, whether on a physical or virtual machine. Therefore, the process of migrating the SQL databases from the Azure VM to a SQL Database or SQL Man¬aged Instance installation can use any of the tools discussed earlier for an on-premises to cloud migration, such as Azure Database Migration Services or Azure Migrate.
Migrating Azure to Azure
To migrate databases from one Azure SQL Database installation, such as to create failover databases in other geographic regions, for example, administrators can open a database in SQL Server Management Studio and export the data to another SQL Database installation using the SQL Server Import and Export Wizard, as shown in Figure 1-54.

FIGURE 1-54 The SQL Server Import and Export wizard
 
Chapter summary

■	Azure supports SQL database deployments with a variety of products, including Azure SQL Database, Azure SQL Managed Instance, and standard Azure virtual machines run¬ning SQL Server on them.
■	Azure Resource Manager (ARM) supports the use of templates to deploy SQL data¬bases in the Azure cloud. Administrators can also use ARM templates to automate SQL deployments using Azure CLI or PowerShell scripts.
■	A hybrid SQL database solution creates a connection between an on-premises SQL Server installation (physical or virtual) and the Azure SQL products available in the cloud.
■	Partitioning and sharding are techniques for splitting tables and storing the pieces in different databases to enhance query performance.
■	Azure SQL Database supports service tiers using two purchasing models: database transaction unit (DTU) and vCore. There is also a separate compute tier with Provisioned and Serverless options. The Provisioned tier allocates compute resources and charges an hourly rate per vCore. The Serverless tier causes Azure to allocate compute capacity as needed and charge a compute cost per vCore second.
■	Azure SQL Managed Instance supports three service tier options: General purpose; Next-gen General Purpose, with improved performance; and Business critical, with much better performance and three added replicas.
■	When configuring an Azure VM running SQL Server, there is a dropdown containing dozens of images, which include various Windows and Linux operating system versions combined with SQL Server versions going back to 2012.
■	When preparing for a database migration from on-premises servers to the Azure cloud, administrators should consider the compatibility levels of the various SQL products involved, the resources the databases will require, and whether the organization can tolerate the downtime needed for an offline migration. If not, an online migration might be necessary.
■	Azure provides a variety of database assessment and migration tools, including Azure Migrate, Azure Database Migration Services (DMS), and Azure Data Studio with the Azure SQL Migration Extension installed.

Thought experiment

In this thought experiment, demonstrate your skills and knowledge of the topics covered in this
chapter. You can find the answers in the section that follows.
Ralph is the SQL database administrator for an organization with multiple on-premises SQL Server installations. The company is expanding, but the datacenter is currently running at its physical capacity and cannot support any additional servers. It has been suggested that the
 
company expand its SQL implementation by creating a new database in the Azure cloud, but Ralph is concerned that he has no experience with cloud technology. With this in mind, con¬sider the following questions about Ralph’s possible SQL expansion to the cloud.
1.	Which of the following initial Azure SQL deployment options should Ralph consider to expand the company’s database implementation, while remaining as close as possible to his SQL administrative experience?
A.	Use Azure SQL Database to deploy a new database.
B.	Create an Azure virtual machine and install SQL Server on it.
C.	Create an Azure SQL Managed Instance.
2.	Which of the following platforms would provide Ralph with the greatest freedom to
configure a cloud server’s operating system, IaaS or PaaS?
3.	After deploying a database instance in the cloud, which of the following techniques can Ralph use to expand its capacity without creating additional servers?
A.	Scaling up
B.	Sharding
4.	Ralph is considering a SQL database migration from an on-premises server to a cloud-based implementation. Which of the following tools actually performs the migration?
A.	Azure Migrate
B.	Azure Data Studio
C.	Azure Database Migration Service

Thought experiment answers

This section contains the solution to the thought experiment. Each answer explains why the answer choice is correct.
1.	B. Creating an Azure virtual machine and installing SQL Server on it would be the closest to Ralph’s experience with on-premises SQL servers.
2.	The Infrastructure as a Service (IaaS) platform is the only one of the Azure SQL deployment options that provides the subscriber with full control over the operating system.
3.	A. Scaling up is the process of adding resources to an existing server to enhance its performance. Sharding requires the storage of database partitions in different database instances (also known as scaling out).
4.	C. Azure Migrate and Azure Data Studio are tools that can analyze and coordinate SQL migrations, but both of these tools use Azure Data Migration Service to perform the actual migration.
 





This page intentionally left blank
 





C HA P T E R 2
Implement a secure environment
Some SQL database administrators are hesitant to store their data in the cloud because they believe it to be inherently insecure. Microsoft Azure provides subscribers with multiple options for deploying SQL in the cloud. One of the primary reasons for doing this is to pro¬vide differing approaches to security.

Skills covered in this chapter:
■	2.1: Configure database authentication and authorization
■	2.2: Implement security for data at rest and data in transit
■	2.3: Implement compliance controls for sensitive data

Skill 2.1: Configure database authentication and
authorization

Databases can contain sensitive information of any type, so it is essential that the database management application and the environment in which it runs be securable. The first steps in implementing any sort of security infrastructure are verifying the identities of the users accessing the data and granting each user an appropriate degree of access. These processes are called authentication and authorization.

 
Configure authentication by using Active Directory and
Microsoft Entra ID
On-premises SQL Server installations typically rely on Active Directory Directory Services (AD DS) for authentication and authorization. AD DS uses servers called domain controllers to provide identity and access management to SQL Server and other Windows services and applications.
Azure SQL Database and Azure SQL Managed Instance use Microsoft Entra ID for authen¬tication and authorization. At one time, Entra ID was known as Azure Active Directory, but the fundamental differences between the two security infrastructures justified the name change. Entra ID, for example, supports conditional access and multifactor authentication, which AD DS does not.
When an on-premises SQL Server installation is configured to use Active Directory for authentication, the users’ initial login to Windows also grants them their SQL database access. In the same way, Azure users’ Entra ID logins can grant them access to a SQL Database or SQL Managed Instance installation.
SQL Server authentication
In addition to Active Directory on-premises and Azure Entra ID, all of the Azure SQL products support the native SQL Server authentication found in the Microsoft SQL Server product. This is an independent authentication mechanism with separate usernames and passwords that are stored in the SQL server’s master database or in its user databases. Administrators decide which authentication model to use during the SQL installation.
The native SQL Server authentication is inherently less secure than either Active Directory or Entra ID. Both of the latter use complex infrastructures and specialized security protocols to provide authentication and authorization services without transmitting passwords and other sensitive traffic over the network in a readable form.
Active Directory uses a security protocol called Kerberos and the Lightweight Directory Access Protocol (LDAP) for authentication and authorization traffic, while Azure Entra ID uses HTTPS protocols such as Security Assertion Markup Language (SAML) and OpenID Connect. SQL Server authentication, by contrast, uses no security protocols and transmits usernames and passwords over the network in plain text, which leaves them open to compromise.
Configuring authentication
When a subscriber creates a new Azure SQL Database installation, they configure an authen¬tication method for the new server by opting to use Entra ID authentication by itself, SQL authentication by itself, or both Entra and SQL authentication, as shown in Figure 2-1.
In addition, administrators can configure existing SQL Database and SQL Managed Instance installations to use Entra ID authentication only, thus disabling SQL authentication, by using the interface shown in Figure 2-2.
 
 
FIGURE 2-1 The Create SQL Database Server page in the Azure portal

FIGURE 2-2 The Microsoft Entra ID page for a SQL Database server in the Azure portal
 
Entra identities are required to access Microsoft Azure, so subscribers already have them when they create a new SQL Database or SQL Managed Instance installation. Azure administra¬tors can create and manage Entra identities through the Azure portal or by using the az ad user commands in Azure command-line interface (CLI) or the AzureADUser cmdlets in PowerShell.
For example, a CLI command to create a new Entra user appears like the following:
az ad user create --display-name ann-beebe --password Pa$$w0rd1234 --user-principal-name ann-beebe@outlook.com
In a SQL Database installation, the Azure subscriber specifies an Entra identity to use as the administrator of the server, as shown in Figure 2-3. This account is granted administra¬tive access to the server and all of the databases on that server. Using a group identity for the administrative account is a recommended practice because it eliminates the need to modify the account to accommodate personnel changes.

FIGURE 2-3 The Microsoft Entra admin setting on an Azure SQL Database Overview page in the Azure portal

In an on-premises SQL Server installation that uses Active Directory for authentication, the administrators must create the Active Directory infrastructure first by installing a Windows Server and assigning it the Active Directory Domain Services role to make it a domain control¬ler. Domain controllers store user account information and provide authentication and authori¬zation services for Windows operating systems and applications, including SQL Server.
When installing SQL Server, the Database Engine Configuration page of the Setup Wizard
provides the options to use Windows authentication mode or Mixed Mode, as shown in
Figure 2-4. Selecting Windows authentication mode disables the native SQL Server authentica¬tion mechanism, while Mixed Mode supports both Windows authentication and SQL Server authentication. There is no option to use SQL Server authentication only because users must always log in to Windows, even if they don’t need access to SQL Server and its databases.
 
 
FIGURE 2-4 The Database Engine Configuration page in the SQL Server 2022 Setup Wizard


Create users from Microsoft Entra identities
Microsoft Entra identities enable users to log on to Azure and access its services, but to create a login for SQL Database or SQL Managed Instance from an Entra identity, an administrator must
 
access the master database and use the T-SQL CREATE LOGIN command, with the following syntax:
USE master GO
CREATE LOGIN [username@contoso.com] FROM EXTERNAL PROVIDER; GO
The FROM EXTERNAL PROVIDER clause indicates that the command will create a SQL login from the credentials associated with the Entra identity username in the contoso.com domain.
To create a SQL login that does not directly match the Entra display name, the administrator can add the WITH OBJECT_ID clause to specify the object identifier for the Entra identity, as in the following example:
CREATE LOGIN [username@contoso.com] FROM EXTERNAL PROVIDER WITH OBJECT_ID='4466e2f8-0fea-4c61-a470-xxxxxxxxxxxx';


Configure security principals
In SQL, a security principal is any entity that can request access to SQL server resources and to which administrators can grant the permissions they need to do so. The resources accessed by the security principals are known as securables, and SQL divides the securables into three sepa¬rate scopes: server, database, and schema. There are security principals in SQL at the server level and the database level.
Some of the terms applied to SQL security principals are used differently from those in other computing contexts. For example, in SQL, the terms “login” and “user” are not interchange¬able. Both are security principals, but a login is an identity at the server level, whereas a user is a
database-level identity. These are the two most important security principals in a SQL installation.
Creating logins
As shown in the previous section, administrators can use the T-SQL command CREATE LOGIN to create new logins at the server level. In addition to creating logins from Entra identities (using the FROM EXTERNAL PROVIDER argument), administrators can also create logins for SQL server authentication, as shown in Figure 2-5, by specifying a username and password, as in the following example:
CREATE LOGIN testuser WITH PASSWORD = ‘Pa$$w0rd’;


Creating users
At the database level, the user is the main security principal. A login grants an individual access to the server, but to actually work with a database on that server, the individual must have a database-level user identity, and the login must be mapped to the user.
In T-SQL, the CREATE USER command allows administrators to create database-level user identities, but it must be executed from the context of the database, as shown in Figure 2-6. As with creating logins, administrators can use CREATE USER to create user identities for Entra users by including the FROM EXTERNAL PROVIDER argument.
 
 
FIGURE 2-5 Creating logins in SQL Server Management Studio (SSMS)

FIGURE 2-6 Creating users in SSMS

For an identity that already exists as a login, administrators can use the CREATE USER com¬mand with the FROM LOGIN argument to create a new user identity and map it to the specified login:
CREATE USER testuser FROM LOGIN testuser


Using roles
Role-based security is common in many network environments. Administrators create identities called roles and assign permissions to them. Functionally, roles operate like security groups.
Assigning users to a role causes them to inherit all of the permissions granted to that role. This
 
simplifies the administrators’ task of managing permissions; instead of having to assign permis¬sions to many individual users, they can assign the permissions to a role once and then add users to or remove them from the role as needed.
Administrators can create SQL roles at the server or the database level, depending on which SQL product they are running. All of the Azure SQL products support database roles, but only SQL Server and Azure SQL Managed Instance support server roles. To grant access to objects in a database, administrators must use database roles.
The SQL products contain predefined roles that administrators cannot change, but they also
support the creation of custom roles. Administrators can create a custom role by connecting to a SQL database and executing the CREATE ROLE command in T-SQL, as shown in Figure 2-7. Then, the GRANT command allocates permissions to the new role and the ALTER ROLE com¬mand adds an existing database user as a member of the role. A typical command sequence might appear as follows:
CREATE ROLE [dbusers] GO
GRANT SELECT, EXECUTE ON SCHEMA::Production TO [dbusers] GO
ALTER ROLE [dbusers] ADD MEMBER [testuser] GO

FIGURE 2-7 Creating database roles in SSMS

The predefined roles in a SQL database contain sets of permissions that allow administra¬tors to delegate standard tasks to specific users. The roles built in to a SQL database (on any platform) are as follows:
■	db_accessadmin Allows the creation of new users in the database
■	db_backupoperator Allows users to execute database backups in SQL Server or SQL MI, but not SQL Database
■	db_datareader  Allows users to read all tables and views in the database
 
■	db_datawriter  Allows users to write to all tables and views in the database
■	db_ddladmin  Allows users to create or modify objects in the database
■	db_denydatareader Denies users with other granted permissions the ability to read from the database
■	db_denydatawriter Denies users with other granted permissions the ability to write to the database
■	db_securityadmin  Allows users to grant other users permissions for the database
■	db_owner  Provides users with administrative access to the database
■	public Default role—initially with no permissions—to which all database users are automatically granted membership
The predefined server roles included in SQL Managed Instance and SQL Server (but not SQL
Database) are as follows:
■	sysadmin  Allows full access to any activity on the server
■	serveradmin  Provides access to server-wide configuration settings
■	securityadmin Provides administrative access to server logins and their properties, as well as server and database permissions
■	processadmin Allows members to kill SQL Server processes
■	setupadmin  Allows members to add and remove linked servers using T-SQL
■	bulkadmin  Allows members to execute the BULK INSERT command
■	diskadmin Allows members to manage backup devices in SQL Server
■	dbcreator  Allows members to create and alter any database
■	public Default role with no permissions to which all server logins are automatically granted membership
Both servers and databases have a public role to which SQL adds logins and users automati¬cally. The role has no permissions by default, but unlike the other predefined roles, it’s possible for administrators to add and remove permissions from the public roles.
Azure SQL Database doesn’t have the same built-in server roles as SQL Server or SQL Man¬aged Instance because the SQL Database product does not have a server in the same sense. SQL Database has only a logical server, which exists mainly because certain applications expect to find it there. There are two server roles in SQL Database, however, as follows:
■	dbmanager  Allows members to create new databases
■	loginmanager  Allows members to create new logins at the server level

Configure database and object-level permissions using graphical tools
Users require permissions to access SQL resources, just as they need permissions for file sys¬tems and other protected elements. SQL supports a variety of tools for setting permissions, but
 
the data manipulation language (DML) for all of the SQL platforms, whether on-premises or in Azure, uses four basic permissions for the securable elements in a database, as follows:
■	SELECT  Allows the user to view the data in the securable element
■	INSERT  Allows the user to add data to the securable element
■	UPDATE Allows the user to modify existing data in the securable element
■	DELETE  Allows the user to delete data from the securable element
There are other permissions that are specific to certain platforms. For example, Azure SQL
Database and SQL Server also support the following permissions in addition to the basic four:
■	CONTROL  Grants the principal all rights to the securable
■	REFERENCES Allows the principal to view the securable’s foreign keys
■	TAKE OWNERSHIP Allows the principal to assume ownership of the securable
■	VIEW CHANGE TRACKING Allows the principal to view the securable’s change track-ing setting
■	VIEW DEFINITION Allows the principal to view the definition of the securable
In addition, functions and procedures support the following permissions:
■	ALTER  Allows the principal to modify the definition of the securable
■	CONTROL  Grants the principal all rights to the securable
■	EXECUTE Allows the principal to execute the securable
■	VIEW CHANGE TRACKING Allows the principal to view the securable’s change track-ing setting
■	VIEW DEFINITION Allows the principal to view the definition of the securable
Administrators can grant, revoke, or deny these permissions to logins, users, roles, and other security principals. Granting a permission allows the principal access to the securable, while denying a permission explicitly prevents that access. In the case of permission conflicts, such
as when a user inherits permissions from multiple sources, deny permissions always supersede the granted ones. Permissions are also cumulative, so that if a user receives permissions from multiple sources, the user’s effective permissions reflect the combination of all those sources.
Configuring permissions with T-SQL
The primary tools that administrators use to configure permissions for SQL databases are
T-SQL commands and SQL Server Management Studio (SSMS). The basic syntax for the T-SQL permission commands is as follows:
AUTHORIZATION PERMISSION ON SECURABLE::NAME TO PRINCIPAL;

■	AUTHORIZATION Specifies the verb GRANT, REVOKE, or DENY
■	PERMISSION  Specifies the permission to be granted, revoked, or denied
■	SECURABLE::NAME Specifies the type and name of the securable to which the per-missions will be applied
■	PRINCIPAL  Specifies the name of the security principal to which the permissions will
be applied
 
For example, the following command grants the select and update permissions for a data¬base called testdb to a user called testuser.
GRANT SELECT, UPDATE ON DATABASE:testdb TO testuser

The PERMISSION argument can be any of the permissions listed earlier, with multiple permissions separated by commas. The SECURABLE can be a server or database or any object on a server or in a database, such as a table or a view. When the context of a T-SQL script is unambiguous, the SECURABLE argument can be omitted and the target object referenced by name only. The PRINCIPAL can be any login or user, but many administrators prefer to assign permissions to roles instead and then assign the roles to logins or users.
Administrators should also understand the difference between revoking permissions and denying them. Revoking a permission is essentially removing it, so that it has no further influ¬ence on the securable. For example, the following command revokes all permissions to the testdb database from the user testuser:
REVOKE SELECT, INSERT, UPDATE, DELETE ON DATABASE::testdb TO testuser

As a result of the command, there are no permissions to testdb granted to the testuser user account. However, if testuser receives permissions from a role assignment, those permissions would still be applicable.
Alternatively, using the DENY command instead of REVOKE explicitly forbids the user from working with the securable, as in the following example.
DENY SELECT, INSERT, UPDATE, DELETE ON DATABASE::testdb TO testuser

While the REVOKE command removes the existing permission assignments, the DENY com¬mand creates new permission assignments of a different type. As a result of this command, testuser is expressly forbidden from accessing the testdb database. Even if testuser receives granted permissions from another source, these deny permissions supersede them.
Configuring permissions with SSMS
SSMS provides a graphical interface that administrators can use to configure permissions for databases and objects. For example, administrators can connect to a SQL server, browse to a database object, such as a table, open its Properties dialog, and select the Permissions page, to display the interface shown in Figure 2-8.
In this SSMS interface, administrators can add security principals to the Users or roles box
and configure their permissions using checkboxes that represent the following authorizations:
■	GRANT Indicates that the security principal will receive the selected permission
■	WITH GRANT Indicates that the security principal will receive the selected permission and the ability to grant that permission to other principals
■	DENY Indicates that the security principal will be prevented from exercising the selected permission, even if they are granted the same permission by other means
 
 
FIGURE 2-8 Configuring table permissions by user in SSMS

Administrators can also approach this task from the other direction by selecting a user in a database’s Security\Users folder, opening its Properties, adding entries to its Securables box, such as a table, and configuring their permissions, as shown in Figure 2-9.

FIGURE 2-9 Configuring user permissions by securable in SSMS

Apply the principle of least privilege for all securables
In SQL security, as in all network security, the principle of least privilege states that users, appli¬cations, and other processes should receive only the privileges to securables that they need to
 
perform their allotted tasks, and no more. The objective is for individuals to receive the access
they need without unnecessarily endangering securables.
Obviously, the simplest (and least secure) security solution to implement is to give everyone access to everything, and the most secure solution is to give no one access to anything. The perfect solution lies somewhere between these two extremes.
Role-based access control is one way for administrators to implement the principle of least privilege easily. Granting permissions to individual users is not only more work for administra¬tors than using roles but administrators also tend to lose track of the permission assignments they have made to specific user accounts. Using roles, administrators can assign permissions more consistently.
The predefined roles in the Azure SQL products enable administrators to assess the needs of their users and apply privileges appropriate to their tasks. Azure even warns administrators when applying highly privileged roles. Adding the Owner role to a user, for example, causes Azure to display a message questioning whether a less-privileged role would be adequate, as shown in Figure 2-10.

FIGURE 2-10 Adding privileged administrator role assignments generates a warning in Azure

Another factor to consider when applying least privilege is selecting the correct secur¬ables to which users need permission to perform a specific task. For example, in the case of an application that relies on stored procedures, users only need the EXECUTE permission for those procedures; they do not need permissions for the underlying tables accessed by the procedures.
 
Troubleshoot authentication and authorization issues
Authentication and authorization are processes that run frequently on many SQL installations, and there are many possible reasons why those processes can fail. Usually, the most common causes of authentication failures are administrative, such as incorrect, lost, or forgotten pass¬words. For installations that use multifactor authentication (MFA), the administrative issues can be compounded as users grow accustomed to the new procedures. However, when admin¬istrative factors can be eliminated as a potential cause of authentication failures, it’s time to troubleshoot other possible causes.
Transient issues in communication and Azure processing can affect authentication and authorization, usually delaying them for only a few seconds. Communication interruptions, such as momentary Internet outages, are always a possibility that can occur at any point between the user and the Azure cloud service.
When a “login failed” error message occurs repeatedly, however, administrators can begin troubleshooting the problem by confirming that the login is not disabled. To do this, admin¬istrators can open the sys.sql_logins catalog view in the master database and check the value of the is_disabled column, as shown in Figure 2-11. A value of False indicates that the login is enabled.

FIGURE 2-11 Examining the sys.sql_logins view in the master database in SSMS

If the value of the is_disabled column is True, indicating that the login is disabled, the admin¬istrator can enable it using a T-SQL command like the following:
ALTER LOGIN testuser ENABLE;

If the login does not exist in the sys.sql_logins view at all, the administrator can create it using the CREATE LOGIN command and then create a corresponding database user with the CREATE USER command. If the user already exists but lacks the necessary permissions, adminis¬trators can assign a role to the user with the ALTER ROLE command or use the GRANT com¬mand to assign permissions to the individual user.
 
The Azure services themselves can also incur delays. For example, the PaaS products, such as Azure SQL Database and Azure SQL Managed Instance, can scale according to changes in
their workloads. Processes such as server reconfiguration or virtual machine migration can cause
authentication processes to fail or be delayed temporarily, generating errors such as the following:
■	Cannot open database "%.&#x2a;ls" requested by the login. The login failed.
■	The service is currently busy. Retry the request after 10 seconds. Incident ID: %ls. Code: %d.
■	Cannot process request. Too many operations in progress for subscription "%ld".
Another possible cause of authentication failures is that the database might have reached the limit of its Azure resources. Both storage and compute resources are subject to limitations, and the service can stop when those limits are exceeded, resulting in error messages such as the following:
Cannot process request. Not enough resources to process request. The service is cur¬rently busy. Please retry the request later.
User error is also a possible source of authentication problems, due to the use of an incor¬rect connection string. This is most common in a newly created or updated database that requires users to alter their connection process. To confirm that the connection string is cor¬rect, each PaaS SQL database has a Connection strings page that displays the connections for the various Microsoft Entra and SQL authentication mechanisms, as shown in Figure 2-12.

FIGURE 2-12 The Connection strings page for a SQL database in the Azure portal
 
Manage authentication and authorization by using T-SQL
As noted earlier in this chapter, administrators are required to select an authentication mode when installing a SQL product in Azure. This setting determines whether SQL will use its own internal (and less secure) SQL authentication or Microsoft Entra.
Administrators can change the authentication mode at any time using the graphical inter¬face on the SQL server’s Microsoft Entra ID page in the Azure portal. In SSMS, administrators can open a SQL server’s Properties dialog and select the Security page to display the Server authentication settings shown in Figure 2-13. Administrators must restart the SQL server after modifying the settings.

FIGURE 2-13 The Security page in the Server Properties dialog in SSMS

Finally, it’s possible to manage the SQL authentication and authorization settings using
T-SQL commands. Enabling SQL server authentication during installation creates and activates a login called sa. Selecting Microsoft Entra or Windows authentication during the installation disables the sa login. If an administrator later decides to change the authentication mode to SQL authentication or mixed mode, the sa login remains disabled.
To enable the sa login and set a password for it, connect to the master database and use the following T-SQL commands:
ALTER LOGIN sa ENABLE;
ALTER LOGIN sa WITH PASSWORD = 'Pa$$w0rd';

To change an installation from SQL authentication only to Windows authentication or mixed mode, it is necessary to modify a Windows registry setting. To do this, use a T-SQL command like the following:
EXEC xp_instance_regwrite 'HKEY_LOCAL_MACHINE', 'Software\Microsoft\MSSQLServer\MSSQLServer', 'LoginMode', REG_DWORD, 1;
 
This command changes the authentication mode to Windows authentication only.
To change to mixed mode, use the following command:
EXEC xp_instance_regwrite 'HKEY_LOCAL_MACHINE', 'Software\Microsoft\MSSQLServer\MSSQLServer', 'LoginMode', REG_DWORD, 2;
After changing the mode, the administrator might want to disable the sa login, which is a potential avenue of attack. The command to do this is as follows:
ALTER LOGIN sa DISABLE;



Skill 2.2: Implement security for data at rest
and data in transit

The process of securing an organization’s data must acknowledge the three possible states of data because they present administrators with different security challenges. As the names imply, data at rest refers to the state of data while it’s motionless, stored safely away on an internal or external device. Data in transit (or data in motion) refers to the state of data while
it’s being transmitted from one location to another, either on a private network or the Internet. The third data state, data in use, refers to data that’s currently loaded into RAM or CPU cache memory. Securing data typically means encrypting it, but these states have differing levels of vulnerability. Therefore, SQL provides different means of encrypting sensitive data in its various states.


Implement transparent data encryption (TDE)
Transparent data encryption (TDE) is the default encryption method for data at rest in SQL Server, Azure SQL Database, and Azure SQL Managed Instance. TDE is enabled by default in all newly created Azure SQL and SQL Server databases.
