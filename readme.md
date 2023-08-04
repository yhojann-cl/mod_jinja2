# Jinja2 module for Apache httpd

Apache module for native render Jinja2 templates powered by Python/C API v3.x.
Designed for informative WEB sites and **avoid the abuse of using heavy CMS
systems for simple content**.


## Advantages

- Fast load and low cost in memory for client and server. Save on physical infrastructure.
- Sites are more secure because there's no database or dynamic content that can be hacked.
- Less maintenance involved. No content management system (CMS).


## Tested on

GNU/Linux distributions:

- Ubuntu Server 20.04 LTS.
- CentOS 7.


## Requirements

- Debian o Rhel distribution based.
- Python3.
- Python3 Development headers (*for compilation only*).
- Apache HTTP Development headers (*for compilation only*).
- Jinja2 module for python3.
- Apache httpd evn vars for load python3 library.


## Installation

Compile module and install it using makefile:

```bash
root@server:~# make;
root@server:~# make install;
```

Create enviroment var:

On Debian based, edit `/etc/apache2/envvars` and write:
`export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libpython3.8.so`.

On Rhel based, edit `/etc/sysconfig/httpd` and write
`export LD_PRELOAD=/usr/lib64/libpython3.so`.

For find python3 library on other systems you can use:
`find / -iname "libpython3*"`.

For validate installation before restart use `apachectl configtest`:

```bash
root@server:~# apachectl configtest;
Syntax OK
```

And, restart server:

For Debian based use `systemctl restart apache2`.

For Rhel based use  `systemctl restart httpd`.


## Uninstallation

Use makefile:

```bash
root@server:~# make uninstall;
```


## How to use?

It's very simple, you make a `.j2` file like as `php` file and use the document
root (`public_html`) as Jinja2 root path. By example:

Code for `index.j2`:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>My Website</title>
    </head>
    <body>
        {% include '/header.html' %}
        <h1>Title</h1>
        <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus
            scelerisque nec est eu condimentum. Cras nec risus diam.
        </p>
        {% include '/footer.html' %}
    </body>
</html>
```

For more info check out the [Jinja2 documentation](https://jinja.palletsprojects.com/en/3.0.x/templates/).

## Available variables

- `os` is the Python3 `os` module.
- `io` is the Python3 `io` module. Useful for calling native file manipulation functions like `io.open()`.
- `datetime` is the Python3 `datetime` module.
- `time` is the Python3 `time` module.
- `re` is the Python3 `re` module.
- `json` is the Python3 `json` module.
- `glob` is the Python3 `glob` module. Useful for get specific files and folder in one line.
- `filename` is the real filename loaded (not the rewrited URL).
- `document_root` is the main public HTML folder of Apache Server (`DocumentRoot` directive).
- `uri` is the full request uri, by example `/abc/def.j2?ghi=jkl`.

And all other Jinja2 native variables, filters and blocks.

