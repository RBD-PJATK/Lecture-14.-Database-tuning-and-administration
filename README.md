# Lecture 14. Database tuning and administration

<h3>Abstract</h3>

<p>This lecture is devoted to two related issues: <i>database administration</i>
and <i>database tuning</i>.  We use MS Access as the example database system.</p>

<p>We start from exploring tuning options available in MS Access and the we present
the list of universal guidelines how to speed up the database.</p>

<p>Then we consider the basic duties of a database administrator.  The administrator:</p>

<ol>
<li>backs up the database,
<li>recovers from failure,
<li>compacts the database,
<li>repairs the database,
<li>converts the database from previous versions of MS Access,
<li>encrypts and decrypts the database,
<li>documents the database, 
<li>manages the replicas of the database,
<li>transforms the database to the client-server model,
<li>protects the database against unauthorized usage.
</ol>

<p>We also discuss the options concerned with the concurrent access by many users and the 
locking of database objects.</p>

<p>The architecture and performance of database management systems and more guidelines for
the administrator will be presented during the sequel lecture <i>Database systems</i>.</p>

<hr><h3><b><a name="Dostrajanie"/>Tuning MS Access</b></h3>

<p>MS Access provides two windows with options. One of them contains options associated with
the start of the MS Access application, while the other window has options that influence
the performance of the MS Access application.</p>


<hr><h3><a name="Opcja">Startup</a></h3>

<p>If you want to open this window, select the menu item "Tools -&gt; Startup".</p>

<p align="center"><img border="0" src="https://gakko.pjwstk.edu.pl/materialy/2398/lec/wyklad14/images/13_1.png"></p>

<p>Here is the explanation of the options of this window.</p>

<dl>
<dt><i>Application title</i>
<dd>The text displayed as the title of the window. It also appears on the task bar.
<dt><i>Application icon</i>
<dd>The icon associated with the database. It also appears besides the application title.
<dt><i>Menu Bar</i>
<dd>The global menu bar to be used.
<dt><i>Shortcut Menu Bar</i>
<dd>The global shortcut menu bar to be used.
<dt><i>Display Form/Page</i>
<dd>The form/page that will be displayed when the user opens the database.
<dt><i>Display Database Window</i>
<dd>If cleared, the database window will be hidden for the users.
<dt><i>Display Status Bar</i>
<dd>If cleared, the window status bar will be hidden from the users.
<dt><i>Use Access Special Keys</i>
<dd>If cleared, the user cannot use:
	<ul>
	<li>F11 to display the database window,
	<li>CTRL+F11 to display the standard menu bar,
	<li>CTRL+BREAK to stop the code and display the current module.
	</ul>
</dl>
 
<p><b>Warning:</b>If the user presses SHIFT at the start of the database, the options set
	in the window <i>Startup</i> will not be taken into account.</p>

<table><tr><td class="notec">Consider using startup options in the database
application you are preparing in the lab.</table> 

<hr><h3><a name="Opcje">Options of Microsoft Access</a></h3> 

<p>If you want to open the window Options, select the menu item "Tools -&gt;
Options".  Among the large number of options that can be set by the
application designer there are three options frequently switched on and off
by the application. These options drive the confirmations.  They are
located in the <i>Confirm</i> frame. You can decide whether MS Access will ask
for confirmation of <i>Record changes</i>, <i>Document deletions</i> and
<i>Action queries</i>.</p>

<p align="center"><img border="0" src="https://gakko.pjwstk.edu.pl/materialy/2398/lec/wyklad14/images/13_2.png"></p>

<table><tr><td class="notec">Reflect on the need for the confirmation
of the updates in your application.  Design this aspect properly in your application.</table> 

<h3><a name="Przyspieszanie">Improving performance of the database application</a></h3>
 
<p>Here is a list of steps that can lead to better performance of your database application.</p>

<ol>
<li>Improve the parameters of hardware (e.g. buy more memory).
<li>Optimize the settings of MS Windows (e.g. extend virtual memory). 
<li>Optimize the settings of the database system (here: MS Access).
<li>Open single-user databases in the exclusive mode (remember that other users cannot use this database).
<li>Normalize the schema of the database (make it third normal form = 3NF).
<li>Create indexes for fields that are frequently used in searches.
<li>Apply the <i>Performance Analyzer</i> (the menu item "Tools -&gt; Analyze -&gt; Performance") to 
	find (and possibly correct) potential faults, e.g. non-compiled code, non-related tables,
	missing index etc.
<li>Apply the <i>Table Analyzer</i> (menu item "Tools -&gt; Analyze -&gt; Table") to 
	find the tables that have redundant data, i.e. are not 3NF.  This tool offers the possibility
	to split these tables into parts.
<li><a name="mde-file"/>
	Convert the database to .MDE format. In this format all modules get compiled; the database gets
	compacted and optimized; useless items (like source code) are dropped. 
	This conversion can be done, when the database is closed.  Select menu item
	"Tools -&gt; Database Utilities -&gt; Make MDE File...".  The design of forms, reports and modules
	of a database in this format cannot be changed.  If such changes are needed, you will have to make
	them in the original database and then convert it again to the .MDE
	format.
<li>Minimize the usage of large objects like wallpapers, OLE objects, graphics. If it is possible,
	convert OLE objects to pictures.
<li>If you want to enter data, open a form in the data entry mode and not in the edit mode.
<li>Use auxiliary tables to store derived data items that are calculated frequently.
	Make these tables be row sources of forms and reports. 
<li>Use queries instead of direct SQL because queries are compiled. Display necessary columns only.
	Do not display columns used only in WHERE conditions.
<li>Frequently <i>compact</i> your hard drive and database. After multiple deletions
	a database may be fragmented which leads to non-optimal usage of disk space.
	<a name="kompaktyfikacji"/>To compact the database, use menu item "Tools -&gt; Database Utilities
	-&gt; Compact and Repair Database...". 
<li>If it is possible, use imported tables instead of linked tables.
<li>Use queries and not SQL statements as row sources of list boxes.
<li>The completed application can be converted into a distribution version.  Users
	of such a version need not install MS Access.  The distribution version
	can be created with the package <i>Microsoft Office 2000 Developer</i>.
</ol>

<table><tr><td class="notec">
Analyze the list presented above and try to apply its items to your application.
</table> 

<hr><h3><a name="Administrowanie">Administering the database</b></a></h3>

<p>We will discuss major duties of a database administrator. He/she:</p>

<ol>
<li>backs up a database,
<li>recovers from failure,
<li>compacts the database,
<li>repairs the database,
<li>converts the database from previous versions of MS Access,
<li>encrypts and decrypts the database,
<li>documents the database, 
<li>manages the replicas of the database,
<li>transforms the database to the client-server model,
<li>protects the database from unauthorized usage.
</ol>

<p>We will also consider the options that drive concurrent usage access to the database
by many users and the related problem of object locks.</p>

<hr><h3><a name="Kopia zapasowa">Backup and recovery</a></h3>

<p>A failure may damage a file which contains a database. 
This failure might be the result of a crash of a disk or power failure
(a user might thoughtlessly switch the machine off!) 
that occurred while the database was open.  The simplest way to backup the database is
to make copies of database files (.MDE and .MDB, registered libraries) and
workgroup files (.MDW - in MS Access it is <code>system.mdw</code>).  You should move 
these copies to a separate medium.  After a failure, just copy these files to their 
original places.</p>

<p align="center">
<table><tr><td class="notec">
Did you make backups during the development of your application?
If not, do it immediately.  Copy the files to at least two other places, so that they are
protected against failures of the database and the disk.
</table> 

<hr><h3><a name="Defragmentacja">Compaction and repair</a></h3>

<ol>
<li>Objects of a database are continuously inserted and deleted.  This causes fragmentation
	of free space on a disk. The compaction the database reduces the size of its file and
	improves its performance.
<li>Sometimes a database file gets damaged, e.g. when the machine is switched off
	while the database
	is still open. In such cases, when you open the database again, MS Access will ask if you
	want it to repair the damaged file automatically.  Sometimes MS Access is unable to detect
	faults and if they are present, you have to initiate the repair yourself. 
</ol>

<p>To compact and repair a database, choose the menu item "Tools -&gt; Database Utilities -&gt;
Compact and Repair Database".</p>

<table><tr><td class="notec">
Compact and repair your application and check how much the size of the database file .MDB has
been reduced.
</table> 

<hr><h3><a name="Konwersja">Conversion from previous version of MS Access</a></h3>

<p>When you install a new version of MS Access, you will have to possibilities
what to do with a database developed with the old version.</p>

<ol>
<li>You can use this database without any conversion. However, then you can change
	neither the design of the database nor the design of their objects.
<li>You can convert this database to the new version of MS Access. 
	However, then you cannot use the old version of MS Access.
</ol>

<p>To convert the database, choose menu item "Tools -&gt; Database Utilities -&gt;
Convert Database".</p>

<hr><h3><a name="Szyfrowanie">Encrypt and decrypt</a></h3>

<p>If you encrypt a database, it cannot be read outside MS Access. MS Access is slower
by 10-15% for encrypted databases.  While MS Access is encrypting a database, it must be closed.
To encrypt or decrypt the database, choose menu item "Tools -&gt; Database Utilities -&gt;
Encrypt/Decrypt Database".</p>


<hr><h3><a name="Dokumentacja">Documenting the database.</a></h3>

<p>MS Access can create a report on selected database objects.  Such a report can be printed
or saved into a text file or stored in a database table.
To document the database, choose menu item "Tools -&gt; Analyze -&gt;
Documenter".</p>

<table><tr><td class="notec">Use the Documenter to document your application.</table> 

<hr><h3><a name="Obix">System objects</a></h3>

<p>If you want to see system tables that store information on a database called
<i>the data dictionary</i> or <i>metadata</i>, select menu item "Tools -&gt; Options", 
activate tab "View" and tick the "System objects" check box.</p>

<p align="center"><img border="0" src="https://gakko.pjwstk.edu.pl/materialy/2398/lec/wyklad14/images/13_3.png"></p>

<table><tr><td class="notec">Inspect the system objects of your application.</table> 

<hr><h3><a name="Replikacja">Database replication</a></h3>

<p>In a distributed environment part of data is shared.  This part
rarely changes and can be replicated in a number of nodes. For each node there
is also part of data used solely at this node.  This part is not
replicated.  This method makes the data closer to the end user and
accelerates the the transactions and queries executed inside the network. 
Even if a network connection is broken, a user can access a locally
stored copy of company data.</p>

<p>A replica may serve as the data source for time consuming reports and backups that normally
would preempt the users' tasks.</p>

<p>Replication cannot be used if the data must always be up to date or
	there are a lot of updating transactions on replicas.</p>

<h4>Replication is MS Access</h4>

<p>In MS Access one database is distinguished as <i>the template</i> which is synchronized
with a number of <i>replicas</i>.  The replicas are also databases. The design of replicated
database objects of the replicas cannot be changed.  However, you can create, delete and modify
local objects in the replicas.</p> 

<p>To create a replica of a database, choose the menu item "Tools -&gt; Replication -&gt;
Create Replica". To synchronize the replica with the template, 
choose the menu item "Tools -&gt; Replication -&gt; Synchronize Now".
If there are replication conflicts, you will have to solve them manually by choosing one 
of the conflicting records.</p>

<p>The size of a replicated database significantly increases and its performance is much worse.</p>

<hr><h3><a name="Praca w sieci">Client/server</a></h3>

<p>The partition of a database into parts of the client and the server has many
advantages:</p>

<ol>
<li>Network traffic is reduced.
<li>It is easier to manage the parts than the whole. The administrator cares for the data,
	while the user cares for the application and he/she can change it
	independently.
</ol>

<p>The database file gets split into two .MDB files:</p>

<dl>
<dt><i>front-end</i> (the client)
<dd>It contains forms, reports, modules and queries.
<dt><i>back-end</i> (the server)
<dd>It tables and queries.
</dl>

<p>If we want to create a client/server application, we will have two choices.
We can build tables and link them to the application that is separate, or
we can put all objects into one .MDB file and then call the Splitter. To start the splitter,
select menu item "Tools -&gt; Add-Ins -&gt; Database Splitter".</p>

<h4>SQL Server</h4>

<p>To store data in the SQL Server is an option that should be considered
seriously when a database gets bigger and bigger. We can move tables and
queries to the SQL Server by means of the <i>Upsizing Wizard</i>.  To fire it,
select menu item "Tools -&gt; Database Utilities -&gt; Upsizing Wizard".</p>

<p>After the database has been upsized we no longer develop
an <i>MS Access database</i>, but we have <i>an MS Access project</i>. 
The user interface (forms, reports and modules) remains in the MS Access database, while
the responsibility for the data storage is transfered to the large database server.
We will present two numbers to compare them. MS Access can run the database up to 2GB, while
the analogous limit for SQL server is 2TB.</p>

<table><tr><td class="notec">
If you have not split your application yet, do it now twice: once manually and 
once by means of the </i>Database Splitter</i>.</table> 

<hr><h3><a name="Blokowanie">Locking data</a></h3>

<p>In MS Access locks concern two levels: database locks and record locks.</p>

<h4>Default open mode for the database</h4>

<p>Users can open a database in one of two modes: <i>Shared</i> and
<i>Exclusive</i>.  When a user just opens a database, the default mode
will be used.  You can set the default mode by means of the menu item "Tools
-&gt; Options".  After you select it, activate tab "Advanced" and set the
<i>Default open mode</i> appropriately to either <i>Shared</i> or
<i>Exclusive</i>.</p>

<p>The exclusive mode should be reserved for the administration activities, e.g.
the encryption or the compaction.

<h4>Record locks</h4>

<p>Forms, reports and functional queries have the property <i>Record Locks</i> that drives
locking records in these database objects.</P>

<dl>
<dt><i>No Locks</i> (the default) also called <i>optimistic locking</i>
<dd>Two or more users can edit the same record at the same time. When they try to
save the changes, MS Access will notify the user that does it as the second
one. This
second user can cancel the changes, copy them to the clipboard or save his/her
changes and thus overwrite the changes of the first user.

<dt><i>All Records</i>
<dd>When a user opens an object, all records of its base tables are locked. Other
users can read the records, but they cannot add, remove 
and update the records of the base tables until the object is closed.

<dt><i>Edited Record</i> also called <i>pessimistic locking</i> (only forms and queries)
<dd>When a user starts editing a field, the whole disk page with this field is locked.
It remains locked, until the user moves to another record.  Therefore, only one user
can edit one record at the same time.  He/she also blocks access to other objects
stored on the same disk page (2 KB).
 
</dl>

<hr><h3><a name="Zabezpieczanie">Protecting the database</a></h3>

<p>An MS Access database can be protected in two ways.</p>

<ul>
<li>You can set the database password.
<li>You can set the protection at the user level.  This means that you define users
	and grant privileges on various objects to these users.
</ul>

<p>Furthermore, you can remove the VBA source code from the database and disallow changing the design
	of forms, reports and modules. In order to do it, create
	<a href="#mde-file">an .MDE file</a>.</p>

<table><tr><td class="notec">
Convert the database to an .MDE file. Check what options are now unavailable.
Verify that the size of the .MDE file has been significantly reduced, when you compare
it with the .MDB file.
</table> 

<hr><h3><a name="Ustalenie">Database password</a></h3>

<p>The password is the simplest way of protection. After the password has been set,
when a user opens the database, it displays the dialog box and requests the valid
password.  This method is safe, because the password is encrypted on the disk.
Therefore no one can find this password by the scan of the database file.
However this password protects only the opening of the database. It is sufficient,
only if the group of users of this database is very small.</p>

<p>To set the database password, choose the menu item "Tools -&gt; Database Utilities -&gt;
Set Database Password".</p>

<p>You must not set the password for a replicated database. If you do, the replicas
will no longer be synchronized.</p>

<table><tr><td class="notec">Do you want unauthorized persons to use
your application?  Set the database password, so that only you and your friends
whom you tell the password can use the database.</table> 

<hr><h3><a name="Zabezpieczenia">User level protection</a></h3>

<p>If the database is protected on the user user level, users log into the database 
with their usernames and passwords.</p>

<p>Users' privileges are managed by means of user groups. The administrator creates
groups and assigns users to these groups. The privileges are granted to groups.
A user has all the privileges of his/her group.</p>

<p>There are two built-in groups: <i>Users</i> and <i>Administrators</i>.
Of course the administrators can define other groups.</i>

<p>A group is granted privileges to perform certain operations on certain
database objects. For example, members of the <i>Users</i> groupmight be
allowed to view, insert and update rows of the <i>Customers</i> table.  However,
the could not alter its design.  These users can only view data of the
<i>Orders</i> table, but they have no privileges on the <i>Payments</i>
table. Members
of the <i>Administrators</i> grouphave all privileges on all database objects. 
You can develop your own authorization system.  In order to do it, you
create user groups with appropriate privileges and then you assign users to
these groups.</p>

<hr><h3><a name="Tworzenie">Users, groups and privileges</a></h3>

<p>If you want to create a group or a user, select the menu item 
"Tools -&gt; Security -&gt; User and group accounts".</p>

<p>After you set the password for user <i>Admin</i>, MS Access will ask users to
provide their usernames and passwords when they log in.</p>

<p>If you want to grant privileges on database objects to a group or a user, 
select menu item 
"Tools -&gt; Security -&gt; User and Group Permissions".</p>

<p align="center"><img border="0" src="https://gakko.pjwstk.edu.pl/materialy/2398/lec/wyklad14/images/13_4.png"></p>

<p>It is recommended to assign privileges to groups and not users. 
Then you assign users to appropriate groups. If you follow this advice,
the process of database administration will be simpler.</p>

<hr><h3><a name="SQL">Users, groups and privileges in SQL</a></h3>

<p>You can also create users and groups and grant privileges by means of SQL.</p> 

<pre><code>CREATE GROUP <i>group group_id</i>;</code>
<code>CREATE USER <i>username password user_id</i>;</code>
<code>ADD USER <i>username</i> TO <i>group</i>;</code>
<code>GRANT <i>privilege</i> ON TABLE <i>table</i> TO [<i>group|username</i>];</code></pre>

<p>Instead of <code><i>privilege</i></code> type <code>SELECT</code>,
<code>INSERT</code>, <code>UPDATE</code>, <code>DELETE</code>, etc.</p>

<p>To revoke a privilege, use the following statement.</p>

<pre><code>REVOKE <i>privilege</i> ON TABLE <i>table</i> FROM [<i>group|username</i>];</code></pre>

<hr><h3><a name="Grupa robocza">Workgroups</a></h3>

<p><i>A workgroup</i> is a group of concurrent users that share data.
Members of a workgroup are described in <i>workgroup files</i>. This file
contains the definitions of groups and the users that drive the user
level protection in MS Access. Their passwords are also stored in this file.
However, information on privileges is stored in databases.  During the
installation of MS Access, a default workgroup is automatically created.
It is described in <i>the default workgroup file</i> named
<code>system.mdw</code>.</p>

<p>Program <code>Wrkgadm.exe</code> (the workgroup administrator) allows:

<ul>
<li>creating a new workgroup (and its workgroup file) and
<li>assigning the locally installed version of MS Access to the selected workgroup
	(next time you start MS Access, it will use this workgroup's file).
</ul>

<hr><h3><a name="Podsumowanie">Summary</a></h3>


<p>We considered two related issues: <i>database administration</i>
and <i>database tuning</i>.</p>

<p>The basic duties of a database administrator are: 
to back up the database,
to recover from failure,
to compact the database,
to repair the database,
to convert the database from previous versions of MS Access,
to encrypt and decrypt the database,
to documents the database, 
to manage the replicas of the database,
to transform the database to the client-server model and 
to protect the database from unauthorized usage.
</p>

<hr><h3><a name="Slownik">Dictionary</a></h3>

<dl>

<dt><a href="#Kopia zapasowa">backup</a>
<dd>Copies of a .MDB file and other related files stored in a safe place.
<dt><a href="#Praca w sieci">client/server</a>
<dd>The model of applications. It consists in the partition of a database into
	two sides: the client and the server. The client provides the user interface,
	while the server stores and provides the data. There are two fundamental
	architectures: both the client and the server are MS Access databases or
	the client is an MS Access databases but the server is run by SQL Server.
<dt><a href="#kompaktyfikacji">compaction</a>
<dd>The process that consists in the defragmentation of free disk space in a 
	database file. Compaction reduces the size of the database file and
	improves the performance of the database.
<dt><a href="#Tworzenie">database user</a>
<dd>A person authorized to access a database.  He/she usually is assigned
	the username and the password.  He/she uses them during login.
<dt><a href="#Dokumentacja">documentation</a>
<dd>A report on all database objects or a subset of them. 
<dt><a href="#Szyfrowanie">encryption</a>
<dd>Encryption of a database file so that it cannot
	be read outside of MS Access.
<dt><a href="#Kopia zapasowa">failure recovery</a>
<dd>In the case of MS Access it consists in copying  all files of
	the backup to their original places. 
<dt><a href="#Blokowanie">lock</a>
<dd>It forbids other users to access an object, when the locking user start to read or
	write this object.
<dt><a href="#mde-file">MDE</a>
<dd>The format of database files of MS Access. In this format all modules gets compiled;
	the database gets compacted and optimized; useless items (like source code) are dropped.
<dt><a href="#Tworzenie">privilege</a>
<dd>A permission granted to a user to perform an operation on a database object, e.g
	to read rows of table <i>Customers</i>. 
<dt><a href="#Zabezpieczanie">protection</a>
<dd>It consists in forbidding unauthorized users to access the database.
<dt><a href="#Replikacja">replica</a>
<dd>A database that contains copies of objects whose originals are stored in another
	database called <i>the template</i>.
<dt><a href="#Obix">system object</a> (data dictionary, metadata)
<dd>A system table that stores information on the database.
<dt><a href="#Przyspieszanie">tuning</a>
<dd>The process that consists of steps the improve the functionality and the
	performance of a database.
<dt><a href="#Tworzenie">user group</a>
<dd>A group of database users recognized by a database. All members of a group
	have the same privileges.
<dt><a href="#Grupa robocza">workgroup</a>
<dd>A group of concurrent users of MS Windows. Its members share the data.
 
</dl>
