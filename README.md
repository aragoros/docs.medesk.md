docs.medesk.md
==============

User's guide and API references

Markdown vs reST
----------------

Unfortunately, Sphinx uses reStructured Text format, which is quite unusual and strage for those who used Markdown. Here is the cheat-sheet to help you:

http://www.unexpected-vortices.com/doc-notes/markdown-and-rest-compared.html

Development
--------------

- Install ReadTheDocs Theme

    pip install sphinx_rtd_theme

    pip install sphinxcontrib-httpdomain

In case of error read [the doc](http://const-cast.blogspot.ru/2009/04/mercurial-on-mac-os-x-valueerror.html)


При ошибках с локалью во время билда:
```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```
