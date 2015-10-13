Профиль
-------

Профиль представляет собой пользователя, способного выполнить вход в систему.
Для предоставления возможности входа, с каждым профилем ассоциируется набор
свойств которые задают его уникальное имя - **логин** и разрешенные механизмы
авторизации.

JSON формат
===========

.. literalinclude:: profile.json
   :language: json

.. -----------------------------------------------------------------------------
.. http:post:: /profiles

  Создает новый профиль.

  **Запрос**:

  .. sourcecode:: http

    POST /profiles HTTP/1.1
    Host: api.medesk.md
    Content-Type: application/json

  .. literalinclude:: profile_create_body.json
     :language: json

  **Ответ**:

  :statuscode 201: Профиль успешно создан. Ответ содержит структуру `информацию <JSON формат_>`_ о созданном профиле.


.. -----------------------------------------------------------------------------
.. http:get:: /profiles/(id)

  Возвращает информацию о профиле.

  **Запрос**:

  .. sourcecode:: http

    GET /profiles HTTP/1.1
    Host: api.medesk.md

  :param id: Идентификатор профиля
  :qparam scopes: Набор покрытий. Доступные заначения:

    - ``general``
    - ``details``
    - ``grants``
    - ``subscriptions``
    - ``memberships``
    - ``calendars``
    - ``private``
    - ``acl``

  **Ответ**:

  :statuscode 200: Успешное выполнение запроса

.. -----------------------------------------------------------------------------
.. http:patch:: /profiles/(id)

  Изменяет заданный профиль.


  **Запрос**:

  .. sourcecode:: http

    PATCH /profiles HTTP/1.1
    Host: api.medesk.md

  :param id: Идентификатор профиля

  **Ответ**:

  :statuscode 204: Успешное выполнение запроса
