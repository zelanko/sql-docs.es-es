---
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
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288096"
---
# <a name="is-odbc-the-answer"></a>¿Es la respuesta ODBC?
Antes de profundizar en la cuestión de la interoperabilidad, considere la siguiente pregunta: ¿Debe la aplicación utilizar ODBC en absoluto? Esto puede parecer una pregunta extraña para hacer en una guía para ODBC, pero es, de hecho, una pregunta legítima. ODBC no se diseñó para reemplazar completamente las API de base de datos nativas, ni estaba diseñado para proporcionar acceso a la base de datos en todas las circunstancias. Fue diseñado para proporcionar una interfaz común a las bases de datos y estaba destinado a liberar a los programadores de aplicaciones de tener que aprender y mantener enlaces a múltiples bases de datos.  
  
 Las aplicaciones personalizadas son los principales candidatos para las API de base de datos nativas. La razón principal es que las aplicaciones personalizadas a menudo funcionan con un solo DBMS y no tienen necesidad de ser interoperables. Las API de base de datos nativas pueden hacer un mejor trabajo que ODBC al exponer las capacidades de un DBMS determinado y pueden exponer capacidades no expuestas por ODBC. Además, dado que los desarrolladores de aplicaciones personalizadas suelen estar familiarizados con la API de base de datos nativa para su DBMS, hay pocas razones para aprender ODBC. Sin embargo, es interesante tener en cuenta que para algunos DBMS, ODBC es la API de base de datos nativa.  
  
 Entonces, ¿qué aplicaciones son candidatas para ODBC? Los mejores candidatos son las aplicaciones que funcionan con más de un DBMS. Esto incluye prácticamente todas las aplicaciones genéricas y verticales. También incluye una serie de aplicaciones personalizadas. Por ejemplo, las aplicaciones personalizadas que usan varios DBMS diferentes son mucho más fáciles y limpias de escribir con ODBC que con varias API nativas. Y las aplicaciones personalizadas escritas con ODBC son mucho más fáciles de migrar a medida que una empresa se mueve de un DBMS a otro o implementa la misma aplicación en diferentes DBMS.
