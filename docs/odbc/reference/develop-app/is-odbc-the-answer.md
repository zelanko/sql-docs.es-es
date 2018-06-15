---
title: ¿Es la respuesta ODBC? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be3439dd75ac7e67fc83c630f9cf0e2ef670a863
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911680"
---
# <a name="is-odbc-the-answer"></a>¿Es la respuesta ODBC?
¿Antes de profundizar en la pregunta de interoperabilidad, tenga en cuenta la siguiente pregunta: debe usar la aplicación a ODBC en absoluto? Esto puede parecer una pregunta extraña debe hacerse en una guía para ODBC, pero es, de hecho, una legítima. ODBC no se diseñó para reemplazar completamente las API de base de datos nativa, ni se diseñó para proporcionar acceso a la base de datos en todas las circunstancias. Se ha diseñado para proporcionar una interfaz común para las bases de datos y se ha diseñado para liberar a los programadores de tener que conocer ni mantener vínculos a varias bases de datos.  
  
 Las aplicaciones personalizadas son candidatos principales para las API de base de datos nativa. La razón principal es que las aplicaciones personalizadas a menudo funcionan con un DBMS único y no tienen que ser interoperable. Base de datos nativa API podrían hacer más eficaces que ODBC de exponer las capacidades de un DBMS concreto y podrían exponer funcionalidades que no se exponen mediante ODBC. Además, dado que los desarrolladores de aplicaciones personalizadas son normalmente familiarizados con la base de datos nativo API para sus DBMS, hay pocas razones para obtener información sobre ODBC. Sin embargo, resulta interesante tener en cuenta que para algunos de los DBMS, ODBC es la API de base de datos nativo.  
  
 ¿Por lo tanto, qué aplicaciones son candidatos para ODBC? Son los mejores candidatos son aplicaciones que funcionan con más de un DBMS. Esto incluye casi todas las aplicaciones verticales y no genéricos. También incluye una serie de aplicaciones personalizadas. Por ejemplo, aplicaciones personalizadas que utilizan varios DBMS diferentes son mucho más fácil y limpio para escribir con ODBC que con las API nativas varios. Y aplicaciones personalizadas creadas con ODBC son mucho más fáciles de migrar a medida que una empresa se mueve de un sistema DBMS a otro o implementa la misma aplicación en diferentes DBMS.
