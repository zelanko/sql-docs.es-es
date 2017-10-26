---
title: Caso de identificador | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c55118fa47337425e715a8b3d6409525668e383f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="identifier-case"></a>Caso de identificador
En las instrucciones SQL y los argumentos de función de catálogo, identificadores y los identificadores entre comillas pueden ser entre mayúsculas y minúsculas o no, que una aplicación puede determinar mediante una llamada a **SQLGetInfo** con el SQL_IDENTIFIER_CASE y SQL_QUOTED_ Opciones de IDENTIFIER_CASE.  
  
 Cada una de estas opciones tiene cuatro valores devueltos posibles: una que indica que el identificador o el caso de identificador entre comillas confidencial y tres indicando que no es confidencial. Los tres valores que no distinguen mayúsculas de minúsculas más describen el caso en el que los identificadores están almacenados en el catálogo del sistema. Cómo se almacenan los identificadores en el catálogo del sistema es relevante solo para fines de presentación, como cuando una aplicación muestra los resultados de una función de catálogo; no cambia la distinción de identificadores.

