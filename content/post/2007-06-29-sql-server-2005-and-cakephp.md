---
author: john
categories:
- General
date: "2007-06-29T10:10:23Z"
guid: http://www.johnmckinzie.com/archives/2007/06/29/sql-server-2005-and-php
id: 76
title: SQL Server 2005 and CakePHP
url: /2007/06/29/sql-server-2005-and-cakephp/
---

Thought I would share the fruits of my labor from trying to get [PHP](http://www.php.net "PHP Website"), specifically [CakePHP](http://www.cakephp.org "CakePHP  PHP Rapid Development Framework "), to connect to a instance of SQL Server 2005 Express. From some initial searches, the only example I found specific to the CakePHP configuration in <tt>databases.php</tt> used [ADOdb](http://adodb.sourceforge.net/ "ADOdb Database Abstraction Library for PHP"). I dowlnoaded the ADOdb library and placed it in the <tt>app/vendors</tt> directory. I was able to successfully connect to the database, however the SQL generate by CakePHP&#8217;s ADO class, had errors and would not probably prepend the field names with the table name.

Looking in CakePHP&#8217;s <tt>cake/lib/model/dbo</tt>, I saw what appeared to be a Microsoft SQL Server class. I was not initially able to connect using the class. With some further research, targeted at PHP&#8217;s <tt>mssql_pconnect</tt>, I found [this MSDN article](http://msdn2.microsoft.com/en-us/library/bb264561.aspx "Accessing SQL Server 2005 Databases with PHP") specifying what port to use and where to find that port in **SQL Server Configuration Manager**. All I had to do is add that port and now I am connecting and generating valid SQL statements. Below is an example configuration file.

<pre>class DATABASE_CONFIG
{
  var $default = array(
                   'driver' => 'mssql',
                   'persistent' => false, //or 'true' for persistent connection
                   'host' => 'localhost', //or ip/DNS
                   'port' => 'port', //the port number obtain from SQL Server Configuration Manager
                   'login' => 'username', //the user of your database
                   'password' => 'password', //the password of your database
                   'database' => 'mydatabase', //the name of your database
                   'prefix' => ”);
}
</pre>