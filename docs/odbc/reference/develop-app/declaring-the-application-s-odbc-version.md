---
title: Declarar la aplicación&#39;s versión de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ea97e3cd7a8fee3b3397524bf2c48c428d6a0be0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076842"
---
# <a name="declaring-the-application39s-odbc-version"></a>Declarar la aplicación&#39;s versión de ODBC
Antes de que una aplicación asigna una conexión, se debe establecer el atributo de entorno SQL_ATTR_ODBC_VERSION. Este atributo indica que la aplicación sigue ODBC *2.x* u ODBC *3.x* especificación al usar los siguientes elementos:  
  
-   **SQLSTATE**. Muchos de los valores SQLSTATE son diferentes en ODBC *2.x* y ODBC *3.x*.  
  
-   **Fecha, hora y los identificadores de tipo de marca de tiempo**. La siguiente tabla muestra los identificadores de tipo de datos de fecha, hora y marca de tiempo en ODBC *2.x* y ODBC *3.x*.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**argumento en SQLTables**. En ODBC *2.x*, los caracteres comodín ("%" y "_") en el *CatalogName* argumento se tratan literalmente. En ODBC *3.x*, se tratan como caracteres comodín. Por lo tanto, una aplicación que sigue a ODBC *2.x* especificación no puede utilizar tal y como caracteres comodín y no realiza escape de ellos cuando se usen como literales. Una aplicación que sigue a ODBC *3.x* especificación puede usarlas como caracteres comodín o ponerlos y usarlos como literales. Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 ODBC *3.x* Administrador de controladores y ODBC *3.x* controladores comprobar la versión de la especificación de ODBC que se escribe una aplicación y responder según corresponda. Por ejemplo, si la aplicación sigue ODBC *2.x* especificación y llama a **SQLExecute** antes de llamar a **SQLPrepare**, ODBC *3.x*Administrador de controladores devuelve SQLSTATE S1010 (función de error de secuencia). Si la aplicación sigue ODBC *3.x* especificación, el Administrador de controladores devuelve SQLSTATE HY010 (función de error de secuencia). Para obtener más información, consulte [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Las aplicaciones que siguen ODBC *3.x* especificación debe utilizar código condicional para evitar el uso de la funcionalidad nueva a ODBC *3.x* al trabajar con ODBC *2.x* controladores. ODBC *2.x* controladores no admiten la funcionalidad nueva a ODBC *3.x* simplemente porque la aplicación declara que sigue a ODBC *3.x* especificación. Además, ODBC *3.x* no dejan de controladores admitir la funcionalidad nueva a ODBC *3.x* simplemente porque la aplicación declara que sigue a ODBC *2.x* especificación.
