Авторизация пользователя
------------------------

Для большинства ресурсов сервиса требуется авторизованный доступ. Это означает
что клиенту необходимо предварительно зарегистрироваться в системе и получить
собственные реквизиты доступа - связка логин/пароль или ``API key``. Далее
клиент должен пройти процедуру авторизации, в рамках которой он выполняет обмен
собственных реквизитов доступа на *токен* доступа и предоставлять его в
последующих запросах.

Авторизация  может быть осуществлена через стандартные процедуры `Resource Owner Password Credentials Grant`_
и `Client Credentials Grant`_, определенные OAuth2.0. Ознакомиться с технологией
OAuth можно прочитав `статью`_, а для более детального понимания нужно
обратиться к `официальной спецификации протокола OAuth2.0`_.

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
    Content-Type: application/json

    {
      "token_type": "Bearer",
      "access_token": "1LiNsBVMfA667Hc3qGpTnlFpRiZrh7tE3yYwjQZevPk=",
      "refresh_token": "YFrqRfwDZP7G3lNPGh1Ci2gRMf9+CPHAA6/LLqHKv6U=",
      "expires_in": 3599
    }

  :>json token_type: Тип токена доступа
  :>json access_token: Токен доступа
  :>json refresh_token: Токен обновления
  :>json expires_in: Количество секунд до истечения срока действия токена доступа.


.. http:delete:: /auth

  Деавторизовать пользователя, удалить рабочую сессию и связанные с ней токены.

  **Запрос**:

  .. sourcecode:: http

    DELETE /auth HTTP/1.1
    Host: api.medesk.md
    Authorization: Bearer w1cqDn72e9cHxnaSxONf+K3L/QjVqVDUoylPEp+ujXc=
    Cache-Control: no-cache

  :reqheader Authorization: OAuth токен

  **Ответ**:

  .. sourcecode:: http

    HTTP/1.1 204 OK

  :statuscode 204: Успешное выполнение запроса


.. http:get:: /auth/mine

  Получить информацию о текущей сессии.

  **Запрос**:

  .. sourcecode:: http

    GET /auth/mine HTTP/1.1
    Host: api.medesk.md
    Authorization: Bearer w1cqDn72e9cHxnaSxONf+K3L/QjVqVDUoylPEp+ujXc=

  :reqheader Authorization: OAuth токен

  **Ответ**:

  .. sourcecode:: http

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "createdAt": "2014-09-05T07:00:04.378Z",
      "updatedAt": "2014-09-05T07:00:22.207Z",
      "expiresIn": 3582,
      "requestsInLastMinute": 14,
      "security": {
        "grantees": [
          "organization{oid=53ce4295d20d470800adfe49}booking-managers#",
          "organization{oid=53ce4295d20d470800adfe49}doctors#",
          "organization{oid=53ce4295d20d470800adfe49}staff#",
          "profile{pid=53ce3a80b48e77c941ea9693}#",
        ]
      },
      "profile": {
        "acl": {
          "general": 15,
          "details": 15,
          "grants": 15,
          "subscriptions": 15,
         "memberships": 15,
         "calendars": 15,
         "private": 15,
         "acl": 15
      },
        "id": "53ce3a80b48e77c941ea9693",
        "url": "/profiles/53ce3a80b48e77c941ea9693",
        "general": {
          "fname": "Иванов",
          "gender": "male",
          "lname": "Иван",
          "mname": "Иванович",
          "timezone": "Europe/Moscow",
          "fio": "Иванов Иван Иванович"
        },
        "grants": {
          "passwordCredentials": {
            "username": "ivanov"
          },
          "clientCredentials": {
            "client": "6sux6DyK"
          }
        }
      }
    }

  :>json expiresIn: Количество секунд до истечения срока действия токена доступа.
  :>json requestsInLastMinute: Количество запросов выполенных за последнюю минуту.
  :>json security: Сведения о группах безопасности связанных с данной сессией.
  :>json profile: Общая информация входящая в покрытие ``general`` профиля с
                  которым связанна сессия.

  :statuscode 204: Успешное выполнение запроса




.. http:patch:: /auth/mine

  Сменить роль в рамках текущей сессии. Изменение роли не изменяет/продлевает время
  жизни текущей сессии.

  **Запрос**:

  .. sourcecode:: http

    PATCH /auth/mine HTTP/1.1
    Host: api.medesk.md
    Authorization: Bearer w1cqDn72e9cHxnaSxONf+K3L/QjVqVDUoylPEp+ujXc=

  :reqheader Authorization: OAuth токен
  :json string membership: идентификатор целевой роли. В случае если значение
    данного параметра равно ``null``, то будет выполнен выход из всех активных
    ролей, а сессия получить набор прав полученный путем пересечения прав всех
    ролей доступных пользователю.

  **Ответ**:

  .. sourcecode:: http

    HTTP/1.1 204 OK

  :statuscode 204: Роль успешно изменена


.. _статью: http://habrahabr.ru/company/mailru/blog/115163/
.. _официальной спецификации протокола OAuth2.0: http://tools.ietf.org/html/rfc6749
.. _Resource Owner Password Credentials Grant: http://tools.ietf.org/html/rfc6749#section-4.3
.. _Client Credentials Grant: http://tools.ietf.org/html/rfc6749#section-4.4
