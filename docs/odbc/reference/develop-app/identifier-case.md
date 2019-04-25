---
title: Caso de identificador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6445cffd5faa8b825c81ec729d7b28c90e14a7b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447827"
---
# <a name="identifier-case"></a>Caso de identificador
En las instrucciones SQL y los argumentos de función de catálogo y entre comillas, puede ser entre mayúsculas y minúsculas o no, que una aplicación puede determinar mediante una llamada a **SQLGetInfo** con el SQL_IDENTIFIER_CASE y SQL_QUOTED_ Opciones de IDENTIFIER_CASE.  
  
 Cada una de estas opciones tiene cuatro valores devueltos posibles: una que indica que el identificador o el caso del identificador entre comillas confidencial y tres indicando que no es confidencial. Los tres valores que no distinguen mayúsculas de minúsculas describen aún más el caso en el que los identificadores están almacenados en el catálogo del sistema. Cómo se almacenan los identificadores en el catálogo del sistema solo es relevante para los fines de presentación, por ejemplo, cuando una aplicación muestra los resultados de una función de catálogo no se cambia la diferenciación de los identificadores.
