---
title: Caso de identificador ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300155"
---
# <a name="identifier-case"></a>Caso de identificador
En instrucciones SQL y argumentos de función de catálogo, los identificadores y los identificadores entre comillas pueden distinguir mayúsculas de minúsculas o no, que una aplicación puede determinar llamando a **SQLGetInfo** con las opciones SQL_IDENTIFIER_CASE y SQL_QUOTED_IDENTIFIER_CASE.  
  
 Cada una de estas opciones tiene cuatro valores devueltos posibles: uno indica que el identificador o el caso de identificador entrecomillado es confidencial y tres indicando que no es confidencial. Los tres valores que no distinguen mayúsculas de minúsculas describen más a fondo el caso en el que se almacenan los identificadores en el catálogo del sistema. La forma en que se almacenan los identificadores en el catálogo del sistema es relevante solo para fines de visualización, como cuando una aplicación muestra los resultados de una función de catálogo; no cambia la sensibilidad de mayúsculas y minúsculas de los identificadores.
