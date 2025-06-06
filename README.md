# Django Lighttpd Middleware

[Django](https://www.djangoproject.com/) is one of the most popular Python web frameworks today.

[Lighttpd](http://www.lighttpd.net/) is, while less popular http server (with that patchy beast [Apache](https://httpd.apache.org/), and that slick new superperformer [nginx](https://nginx.org/en/) dominating the market), the best choice for a web server sometimes.

In a nutshell, Apache is bloated, dated, slow and resource hungry, nginx is slick, lean, fast, scales well. It outperfoms Apache on every relevant measure, and as a consequence has been the rising star in http servers for good reason. Almost everywhere I look web focussed FOSS today comes with instructions on how to run it under Apache (just because) and nginx (because that's what everyone does). Go nginx.

**So when is lighttpd the server of choice?**

I'll leave you to search the reports on-line, they are easy to find,  but lighttpd performs on par with nginx on all measures. Sometimes a litle better, sometimes a little worse. Like nginx it is written from the ground up to be light, slick, fast and scaleable.

The key differences between lighttpd and nginx for me are:

- lighttpd is free (as in free beer, as the saying goes), nginx is freemium (free - and open source - but you can pay for more). Freemium and I have love hate relationship. It's a fatastic business model and I love it. But I don't like running into limits behind paywalls either.
- It is the server of choice in the OpenWRT project when uhttpd isn't enough. OK, so if you're managing a network with OpenWRT routers (and I do, as a gateway, on WAPS, as DHCP server, DNS server, and more) then you have lighttpd to manage there already. In particular the NAT and reverse Proxy configurations you need for serving from behind a firewall and gateway. And if I'm invested in lighttpd there why not stick with it? Why learn another one. Not least when it's just as good, and free, not freemium.

**The black sheep**

That said, lighttpd is the black sheep in the family and while the world of web services is falling over itself to provide Apache and nginx compatibility and guides and installers and more, lighttpd is mostly ignored and does a few things a little differently.

One of those is how it delivers SCRIPT_NAME and PATH_INFO. It's not wrong, it's different to Apache and nginx. And Django is one of those projects where development has presumed Apache or nginx and hence a particular SCRIPT_NAME and PATH_INFO convention (which is not a standardised convention alas and up to the http server).

And so this is middleware for Django (or a wsgi_handler replacement) that maps lighttpd's SCRIPT_NAME and PATH_INFO to Django's expectations.

Just add "django_lighttpd_middleware.LighttpdMiddleware" as the first entry in you MIDDLEWARE tuple and you're good to go. 

`__init__.py` contains more notes in its header for the technically oriented.

