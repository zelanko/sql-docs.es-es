---
title: "Declarar la aplicación &#39; s ODBC versión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32bfeff983ef5dff4ebfe3e575bcf36e855184d0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="declaring-the-application39s-odbc-version"></a>Declarar la aplicación &#39; s versión de ODBC
Antes de que una aplicación asigna una conexión, se debe establecer el atributo de entorno SQL_ATTR_ODBC_VERSION. Este atributo indica que la aplicación sigue la API ODBC 2. *x* u ODBC 3. *x* especificación al usar los siguientes elementos:  
  
-   **SQLSTATE**. Muchos de los valores SQLSTATE son diferentes en ODBC 2. *x* y ODBC 3. *x*.  
  
-   **Fecha, hora y los identificadores de tipo de marca de tiempo**. La siguiente tabla muestra los identificadores de tipo de fecha, hora y datos de marca de tiempo de ODBC 2. *x* y ODBC 3. *x*.  
  
    |ODBC 2. *x*|ODBC 3. *x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo de C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *CatalogName***argumento en SQLTables**.   En ODBC 2. *x*, los caracteres comodín ("%" y "_") en el *CatalogName* argumento se tratan de forma literal. En ODBC 3. *x*, se tratan como caracteres comodín. Por lo tanto, una aplicación que sigue a la API ODBC 2. *x* especificación no puede utilizar como comodín caracteres y no de escape ellos cuando se usen como literales. Una aplicación que sigue a ODBC 3. *x* especificación puede usarlas como caracteres comodín o convertirlos y usarlos como literales. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 ODBC 3*.x* el Administrador de controladores mientras que ODBC 3*.x* controladores comprobar la versión de la especificación de ODBC en el que se escribe una aplicación y responder según corresponda. Por ejemplo, si la aplicación sigue a la API ODBC 2. *x* especificación y llamadas **SQLExecute** antes de llamar a **SQLPrepare**, ODBC 3*.x* Administrador de controladores devuelve SQLSTATE S1010 ( Error de secuencia de función). Si la aplicación sigue ODBC 3*.x* especificación, el Administrador de controladores devuelve SQLSTATE HY010 (error de secuencia de función). Para obtener más información, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Aplicaciones que siguen ODBC 3. *x* especificación debe utilizar código condicional para evitar usar la funcionalidad nueva para ODBC 3. *x* al trabajar con ODBC 2. *x* controladores. ODBC 2. *x* controladores no admiten la funcionalidad nueva para ODBC 3. *x* solo porque la aplicación declara que sigue a ODBC 3. *x* especificación. Además, ODBC 3. *x* no dejan de controladores admitir la funcionalidad nueva para ODBC 3. *x* solo porque la aplicación declara que sigue a la API ODBC 2. *x* especificación.

