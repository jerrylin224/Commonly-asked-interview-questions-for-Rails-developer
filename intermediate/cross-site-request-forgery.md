# Cross-site Request Forgery & csrf\_meta\_tags

## Cross-site Request Forgery

> **Cross-site request forgery**, also known as **one-click attack** or **session riding** and abbreviated as **CSRF **\(sometimes pronounced sea-surf\) or **XSRF** , is a type of malicious exploit of a website from a user that the web application trusts. Unlike cross-site scripting \(XSS\), which exploits the trust a user has for a particular site, CSRF exploits the trust that a site has in a user's browser. - from wiki

Simply put, we can say CSRF is a malicious user induce the **log in **user to send a request to the server to trigger unexpected result. For example, a malicious person want to make a user to delete some information on certain site. The malicious person can send the user a mail including link like "[Get your free iPhoneX today!](/www.apple.com)", but actually the link will send a `Delete` request to the server. If the user has signed in the website, the request will delete the data.

## csrf\_meta\_tags

In Rails, we will add the `csrf_meta_tags` to precent CSRF. The tag will returns meta tags `csrf-param` and `csrf-token` with the name of the cross-site request forgery protection parameter and token, respectively.

