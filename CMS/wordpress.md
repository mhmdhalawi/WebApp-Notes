# WPScan

It helps in enumerating a wordpress website such as:

- Wordpress version
- PHP Version
- Users of the application
- Installed plugins and versions
- Vulnerabilities related to wp and installed plugins
- Additional content (robots.txt, interesting headers,etc)
  
  <br/>
  

        wpscan --url http://fooblog.site

To enumerate users

        wpscan --url http://fooblog.site --enumerate u

To enumerate plugins

        wpscan --url http://fooblog.site --enumerate p


Furthermore, using “curl”, we can confirm we get a proper 404 from a directory that doesnt exist

    # curl -s -o /dev/null -w "%{http_code}\n" http://fooblog.site/author/user

**result is 404**

<br/>

Whereas, using the same curl command, and querying for an known existing user gives a 301 http status.

if the user is found using the above command then the result is **301**

<br/>

# Nmap

     nmap --script http-wordpress-enum fooblog.site
<br/>

# Indexing

use **/wp-content/** to index all the files in the wordpress directory

**url**

    fooblog.site/wp-content/

For **plugins**

    fooblog.site/wp-content/plugins/

<br/>

# Use searchsploit to check for exploits

    searchsploit wordpress responsive thumbnail slider 1.0

**wordpress responsice thumbnail slider** is the plugin name

**1.0** plugin version