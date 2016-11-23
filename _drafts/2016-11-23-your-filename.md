---
published: false
layout: post
date: 2016-11-23T09:16:16.000Z
tags:
  - backend
  - nosql
description: Mémo sur Redis...
categories: backend nosql
serie: bdd
---
## Redis

http://sametmax.com/redis-pourquoi-et-comment/

Vous allez me dire, mais quel intérêt ? Je peux déjà faire ça avec une variable. Certes, mais Redis est accessible depuis n’importe quel programme de votre serveur. Vous pouvez donc facilement partager des valeurs entre vos processus. Par exemple, avec Django, on a souvent plusieurs workers WSGI, et Redis permet donc de partager des informations entre ces workers. Pour cette raison, on peut utiliser Redis pour créer un lock partagé.
