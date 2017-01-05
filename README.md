# ApacheTutorials-Apache
Lets Learn Apache Practically


httpd.conf
Listen 0.0.0.0:80
Listen [::0]:80


httpd-vhost.conf
# Virtual Hosts
#
<VirtualHost *:80>
    ServerAdmin admin@localhost
    #Document base defined which wamp server can identify
    DocumentRoot "c:/wamp64/www/"

    ServerName localhost
    ErrorLog "logs/localhost-error.log"
    CustomLog "logs/localhost-access.log" common

    #wamp server searches for this section
    <Directory "c:/wamp64/www">
        AllowOverride None	
        #Options FollowSymLinks -Indexes
          # UPDATED for Apache 2.4
          # Access Control 
          Require local
    </Directory>
    <Directory "c:/wamp64/www/webservice">    
        AllowOverride None
      #Options FollowSymLinks -Indexes
	Order Allow,Deny
          # UPDATED for Apache 2.4
          # Access Control 
	Allow from howru.com
	Deny from localhost
    </Directory>
</VirtualHost>



<VirtualHost *:80>
    ServerAdmin admin@howru.com
    #Document base defined which wamp server can identify
    DocumentRoot "c:/wamp64/www/webservice/"
    ServerName howru.com
    ErrorLog "logs/localhost-error.log"
    CustomLog "logs/localhost-access.log" common
    #wamp server searches for this section

  <Directory "c:/wamp64/www/webservice/">
      AllowOverride None

          # UPDATED for Apache 2.4
          # Access Control 

   </Directory>
    <Directory "c:/wamp64/www">
        AllowOverride None	
        #Options FollowSymLinks -Indexes
          # UPDATED for Apache 2.4
          # Access Control 
          Require local
    </Directory>
</VirtualHost>
#



windows host file
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
	127.0.0.1       localhost
	127.0.0.1		howru.com 
#TestSite
	

USER AUTHENTICATION

1. Update http.conf by adding :

AccessFileName htaccess.acl .htaccess

2. Add “Directory” tag into http.conf as shown below :

<Directory "c:/wamp/www/basic-auth/"> 
    Options None 
    AllowOverride all 
    Order Deny,Allow 
</Directory>

3. Next step is to create password file.

cd C:\wamp\bin\apache\Apache2.2.11\bin 
htpasswd -c pwd.txt prash


4. Create the htaccess file - htaccess.acl file with the following data.

AuthUserFile C:\wamp\bin\apache\Apache2.2.11\bin\pwd.txt 
AuthName "Protected" 
AuthType Basic
<Limit GET POST> 
require valid-user 
</Limit>

saved this .htaccess file in the folder where you want user authentication

SSL ENABLING IN WEBSITE (http ---> https )

download opensilverlight 64bit windows software

