API
===============

.. ATTENTION::
   Текущая версия API имеет статус *DRAFT* и находиться в постоянной разработке.
   Это означает что часть методов и/или их сигнатур может быть изменена, в связи
   с чем, необходимо следить за изменениями в сервисе.


Авторизация пользователя
------------------------

Задачей авторизации является получения токена безопасности и может быть
осуществлена через процедуры Resource Owner Credentials и Client Credentials
определенные OAuth2.0. Для знакомство с технологией ``OAuth`` советуем
ознакомиться со `статьей`_, а так же обратиться к `официальной спецификации протокола OAuth2.0`_.


.. http:post:: /auth

  Авторизовать пользователя и получить токен доступа ( `Resource Owner Password Credentials Grant`_ )

  **Запрос**:

  .. sourcecode:: http

    POST /auth HTTP/1.1
    Host: api.medesk.md
    Cache-Control: no-cache
    Content-Type: multipart/form-data

  :fparam token_type: тип авторизации
  :fparam password: пароль пользователя
  :fparam username: логин пользователя

  **Ответ**:

  .. sourcecode:: http

    HTTP/1.1 200 OK
    Content-Type: text/javascript

    {
      "token_type": "Bearer",
      "access_token": "1LiNsBVMfA667Hc3qGpTnlFpRiZrh7tE3yYwjQZevPk=",
      "refresh_token": "YFrqRfwDZP7G3lNPGh1Ci2gRMf9+CPHAA6/LLqHKv6U=",
      "expires_in": 3599
    }


.. _статьей: http://habrahabr.ru/company/mailru/blog/115163/
.. _официальной спецификации протокола OAuth2.0: http://tools.ietf.org/html/rfc6749
.. _Resource Owner Password Credentials Grant: http://tools.ietf.org/html/rfc6749#section-4.3
