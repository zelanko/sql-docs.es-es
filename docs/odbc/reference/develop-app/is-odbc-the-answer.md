---
description: ¿Es la respuesta ODBC?
title: ¿Es la respuesta ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476607"
---
# <a name="is-odbc-the-answer"></a>¿Es la respuesta ODBC?
Antes de profundizar en la cuestión de la interoperabilidad, tenga en cuenta la siguiente pregunta: ¿debe la aplicación usar ODBC? Esto puede parecer una pregunta extraña para preguntar a ODBC, pero, de hecho, es legítima. ODBC no se diseñó para reemplazar completamente las API de bases de datos nativas, ni se diseñó para proporcionar acceso a bases de datos en todas las circunstancias. Se diseñó para proporcionar una interfaz común a las bases de datos y se diseñó para que los programadores de aplicaciones no tuvieran que obtener información sobre los vínculos a varias bases de datos y mantenerlos.  
  
 Las aplicaciones personalizadas son candidatas principales para las API de bases de datos nativas. La razón principal es que las aplicaciones personalizadas suelen funcionar con un solo DBMS y no tienen que ser interoperables. Las API de bases de datos nativas pueden hacer un mejor trabajo que ODBC de exponer las capacidades de un DBMS determinado y pueden exponer capacidades que no expone ODBC. Además, dado que los desarrolladores de aplicaciones personalizadas suelen estar familiarizados con la API de base de datos nativa para su DBMS, hay pocos motivos para obtener información sobre ODBC. Sin embargo, es interesante tener en cuenta que, para algunos DBMS, ODBC es la API de base de datos nativa.  
  
 ¿Qué aplicaciones son candidatas para ODBC? Los mejores candidatos son las aplicaciones que funcionan con más de un DBMS. Esto incluye prácticamente todas las aplicaciones genéricas y verticales. También incluye una serie de aplicaciones personalizadas. Por ejemplo, las aplicaciones personalizadas que usan varios DBMS diferentes son mucho más fáciles y más nítidas de escribir con ODBC que con varias API nativas. Y las aplicaciones personalizadas escritas con ODBC son mucho más fáciles de migrar a medida que una empresa pasa de un DBMS a otro o implementa la misma aplicación en distintos DBMS.
