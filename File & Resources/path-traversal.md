let’s consider a Web Application that allows us to download a file by requesting the following URL:

    http://www.elsfoo.com/getFile?path=FileA418fS5fds.pdf

The parameter **path**  will be used by the web application to locate the resource named **FileA418fS5fds.pdf** on the file system.

If the web application does not sanitize the parameter properly, an attacker could manipulate it to access the contents of any arbitrary file.

This attack, also known as the **dot-dot-slash** attack ( **. . /** ) is usually performed by means of those characters that allow us to move up the directory tree.

<br/>

# Example


## Unix

<br/>

    http://www.elsfoo.com/getFile?path=../../../etc/passwd

<br/>

## Windows

    http://www.elsfoo.com/getFile?path=../../../windows/win.ini

    http://www.elsfoo.com/getFile?path=../../../boot.ini

Depending on the Operating System running on the web server, a root folder can be located using the following syntax:

**Unix** : **slash - /**

**Windows** : **&lt;Driver letter> : &#92; - C:&#92;**


The following are the directory separator symbols to use depending on the Operating System:

**Unix** : **Slash - /**

**Windows** : **Slash - / or Backslash - &#92;**