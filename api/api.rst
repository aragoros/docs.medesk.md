MEDESK API
=========================

We have a limited public API that is available for you to get data out of the site. This page will only show a few of the basic parts, please file a ticket or ping us on IRC (#readthedocs on `Freenode (chat.freenode.net) <http://webchat.freenode.net>`_) if you have feature requests.

This document covers the read-only API provided. We have plans to create a read/write API, so that you can easily automate interactions with your project.

The API is written in Tastypie, which provides a nice ability to browse the API from your browser. If you go to http://readthedocs.org/api/v1/?format=json and just poke around, you should be able to figure out what is going on.

A basic API client using slumber
--------------------------------

You can use `Slumber <http://slumber.in/>`_ to build basic API wrappers in python. Here is a simple example of using slumber to interact with the RTD API::

    import slumber
    import json

    show_objs = True
    api = slumber.API(base_url='http://readthedocs.org/api/v1/')

    val = api.project.get(slug='pip')
    #val = api.project('pip').get()

    #val = api.build(49252).get()
    #val = api.build.get(project__slug='read-the-docs')

    #val = api.user.get(username='eric')

    #val = api.version('pip').get()
    #val = api.version('pip').get(slug='1.0.1')

    #val = api.version('pip').highest.get()
    #val = api.version('pip').highest('0.8').get()

    if show_objs:
        for obj in val['objects']:
            print json.dumps(obj, indent=4)
    else:
        print json.dumps(val, indent=4)


API Endpoints
-------------

Feel free to use cURL and python to look at formatted json examples. You can also look at them in your browser, if it handles returned json.

::

    curl http://readthedocs.org/api/v1/project/pip/?format=json | python -m json.tool

Root
----
.. http:get:: /users/(int:user_id)/posts/(tag)

   The posts tagged with `tag` that the user (`user_id`) wrote.

   **Example request**:

   .. sourcecode:: http

      GET /users/123/posts/web HTTP/1.1
      Host: example.com
      Accept: application/json, text/javascript

   **Example response**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Vary: Accept
      Content-Type: text/javascript

      [
        {
          "post_id": 12345,
          "author_id": 123,
          "tags": ["server", "web"],
          "subject": "I tried Nginx"
        },
        {
          "post_id": 12346,
          "author_id": 123,
          "tags": ["html5", "standards", "web"],
          "subject": "We go to HTML 5"
        }
      ]

   :query sort: one of ``hit``, ``created-at``
   :query offset: offset number. default is 0
   :query limit: limit number. default is 30
   :reqheader Accept: the response content type depends on
                      :mailheader:`Accept` header
   :reqheader Authorization: optional OAuth token to authenticate
   :resheader Content-Type: this depends on :mailheader:`Accept`
                            header of request
   :statuscode 200: no error
   :statuscode 404: there's no user
