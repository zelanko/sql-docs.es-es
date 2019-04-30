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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f90f2395eac5dce76848d7bc309f1a3d5ce289f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63179893"
---
# <a name="is-odbc-the-answer"></a>¿Es la respuesta ODBC?
Antes de profundizar en la pregunta de interoperabilidad, tenga en cuenta la siguiente pregunta: ¿Debe la aplicación usa ODBC en absoluto? Esto puede parecer una pregunta extraña en una guía para ODBC, pero es, de hecho, una legítima. ODBC no se diseñó para reemplazar completamente la API de base de datos nativa, ni se diseñó para proporcionar acceso a la base de datos en todas las circunstancias. Se diseñó para proporcionar una interfaz común para las bases de datos y se ha diseñado para liberar a los programadores de aplicaciones de tener que conocer y conservar los vínculos a varias bases de datos.  
  
 Las aplicaciones personalizadas son candidatos principales para las API de base de datos nativo. La razón principal es que las aplicaciones personalizadas a menudo trabajar con un DBMS único y no es necesario para que sea interoperable. Base de datos nativa API podrían hacer mejor su trabajo de ODBC de exponer las capacidades de un DBMS concreto y podrían exponer funcionalidades que no se exponen mediante ODBC. Además, dado que los desarrolladores de aplicaciones personalizadas son normalmente está familiarizados con la base de datos nativo API para su sistema de DBMS, hay pocas razones para obtener información sobre ODBC. Sin embargo, es interesante tener en cuenta que para algunos de los DBMS, ODBC es la API de base de datos nativo.  
  
 ¿Qué aplicaciones son candidatos para ODBC? Los mejores candidatos son aplicaciones que funcionan con más de un DBMS. Esto incluye prácticamente todas las aplicaciones genéricas y verticales. También incluye un número de aplicaciones personalizadas. Por ejemplo, aplicaciones personalizadas que utilizan varios de los distintos DBMS son mucho más fácil y más fáciles de escribir con ODBC que con varias de las API nativas. Y aplicaciones personalizadas creadas con ODBC son mucho más fáciles de migrar a medida que una empresa de un sistema DBMS se mueve a otro o implementa la misma aplicación en diferentes DBMS.
