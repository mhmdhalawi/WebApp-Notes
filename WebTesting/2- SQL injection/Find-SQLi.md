# **Input Parameters**
Input parameters are carried through **GET and POST requests,HEADERS and COOKIES(User-agent,Referer).** So, we have to check all the channels where data is retrieved from the client.

&nbsp;

# Testing an input for SQL injection means trying to inject:

**String terminators:' and "**

**SQL commands: SELECT,UNION and others**

**SQL comments: # or --**

Always test **One injection at a time!** otherwise you will not be able to understand what injection vector is successful.

&nbsp;

# Comment a query
    # the Hash Symbol
    -- two dashes followed by a space

# Union Example
    SELECT  Name, Description FROM Products where ID='3' UNION SELECT Username, Password FROM Accounts

# OR | AND Example
     SELECT Name, Description FROM Products WHERE ID='' OR/AND 'a'='a

