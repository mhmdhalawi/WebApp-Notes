# Lab Example

Login with the following credentials:

- Username: mike

- Password: ABC7d8z1

![cross-domain-data-stealing-lab](images/cdds.png)

You can see that checking account information is stored in JavaScript variables, provided by the URL balance.php. This resource acts as a JavaScript library file so that it can be imported by any web page regardless of its domain origin.

![cross-domain-data-stealing-lab](images/cdds2.png)

## Building the exploit

The attacker can build an html page in a domain under his control. This page will access the JavaScript variables owned by the unlucky bank customer.

The exploit code will have a similar structure:

![cross-domain-data-stealing-lab](images/cdds3.png)

Note that the JavaScript variables can be loaded only if a logged user loads the malicious page. Unauthenticated users will get an empty file.

To be sure the page is loaded by an authenticated user, the attacker can use the Feedback area to spread a link to his malicious web site. A customer opening that link will become a victim.

![cross-domain-data-stealing-lab](images/cdds4.png)

## Running the exploit

Open a second browser (for example Google Chrome), and login with the following credentials:

- Username: jason

- Password: 8AqL168a

![cross-domain-data-stealing-lab](images/cdds5.png)

Go to the feedback area and open the link provided by Mike.

![cross-domain-data-stealing-lab](images/cdds6.png)

The browser will load the JavaScript variables related to the logged session and will steal checking account information:

![cross-domain-data-stealing-lab](images/cdds7.png)

For education purposes, the malicious page will show you all the stolen information. In a real-world attack, this information is secretly retrieved and collected by the attacker.