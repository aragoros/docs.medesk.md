Организации
------------------------

Организации представляют собой юридические лица и могут является публичными или
частными. Различия между публичными и частными организациями определяются
уровнем доступа, которые они предоставляют пользователям системы. Например,
большинство контрагентов организации могут являться частными, в случае
необходимости их сокрытия от других участников платформы, другие же наоборот
могут оставаться публичными, в случае их взаимодействия с другим юридическими
лицами. Примером публичной организации могут являться страховые компании, которые
также предоставляют информацию о выданных полисах индивидуального страхования.


.. http:get:: /enterprises

   Поиск предприятий.

  **Запрос**:

  .. sourcecode:: http

    GET /enterprises HTTP/1.1
    Host: api.medesk.md

  :qparam scopes: Перечень покрытий который должен быть возвращен для каждой
                  найденной организации.
  :qparam q:      Строка поиска
  :qparam limit:  Максимальное число объектов которое должен вернуть запрос;
                  положительное число <=25
  :qparam offset: Позиция с которой начанать поиск; натуральное число включая 0
  

  **Ответ**:

  .. sourcecode:: http

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "id": "53ce4295d20d470800adfe49",
      "url": "/enterprises/53ce4295d20d470800adfe49",
      "acl": {
        "general": 8,
        "system": 8,
        "subscription": 8,
        "configuration": 8,
        "finance": 8,
        "memberships": 8,
        "replication": 8,
        "acl": 0
      },
      "public": true,
      "createdAt": "2014-07-22T10:53:10.094Z",
      "updatedAt": "2014-09-03T19:20:30.106Z",
      "general": {
        "fullName": "Многопрофильный медицинский центр «MEDESK»",
        "name": "Медицинский центр «MEDESK»",
        "tags": [],
        "timezone": "Europe/Moscow"
      },
      "contacts": {
        "emails": [{
          "id": "540762c0f92b0ecb1b7454e7",
          "url": "/enterprises/53ce4295d20d470800adfe49/contacts/emails/540762c0f92b0ecb1b7454e7",
          "value": "support@medesk.md",
          "verified": false,
          "isMaster": false
        }],
        "phones": [{
          "id": "540762c0f92b0ecb1b7454e6",
          "url": "/enterprises/53ce4295d20d470800adfe49/contacts/phones/540762c0f92b0ecb1b7454e6",
          "value": "+7 (499) 677-18-38",
          "verified": false,
          "type": "landline"
        }],
        "website": "http://www.medesk.md"
      },
      "_sm": {
        "_highlight": {},
        "_score": 5.350813,
        "_type": "enterprise"
      }
    }

  :statuscode 200: Успешное выполнение запроса
