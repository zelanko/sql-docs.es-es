---
description: Declaración de la versión de ODBC de Application&#39;s
title: Declaración de la versión de ODBC de Application&#39;s | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ff41a7a8b56133b0a44947980805c5b46238bad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424727"
---
# <a name="declaring-the-application39s-odbc-version"></a>Declaración de la versión de ODBC de Application&#39;s
Antes de que una aplicación asigne una conexión, debe establecer el atributo de entorno SQL_ATTR_ODBC_VERSION. Este atributo indica que la aplicación sigue la especificación ODBC *2. x* u ODBC *3. x* cuando se usan los siguientes elementos:  
  
-   **SQLSTATEs**. Muchos valores SQLSTATE son diferentes en ODBC *2. x* y ODBC *3. x*.  
  
-   **Identificadores de tipo de fecha, hora y marca de tiempo**. En la tabla siguiente se muestran los identificadores de tipo de datos de fecha, hora y marca de tiempo en ODBC *2. x* y ODBC *3. x*.  
  
    |ODBC *2. x*|ODBC *3. x*|  
    |----------------|----------------|  
    |**Identificadores de tipo SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificadores de tipo de C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   Argumento _nombrecatálogo_**en SQLTables**.   En ODBC *2. x*, los caracteres comodín ("%" y "_") del argumento *nombrecatálogo* se tratan literalmente. En ODBC *3. x*, se tratan como caracteres comodín. Por lo tanto, una aplicación que sigue a la especificación de ODBC *2. x* no puede usarlos como caracteres comodín y no los escapa cuando se usan como literales. Una aplicación que sigue a la especificación de ODBC *3. x* puede usarlos como caracteres comodín o escapar y usarlos como literales. Para obtener más información, vea [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 El administrador de controladores ODBC *3. x* y los controladores ODBC *3. x* comprueban la versión de la especificación de ODBC en la que se escribe una aplicación y responden en consecuencia. Por ejemplo, si la aplicación sigue la especificación ODBC *2. x* y llama a **SQLExecute** antes de llamar a **SQLPrepare**, el administrador de controladores ODBC *3. x* devuelve SQLSTATE S1010 (error de secuencia de función). Si la aplicación sigue la especificación de ODBC *3. x* , el administrador de controladores devuelve SQLSTATE HY010 (error de secuencia de función). Para obtener más información, consulte [compatibilidad con versiones anteriores y cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Las aplicaciones que siguen la especificación de ODBC *3. x* deben usar código condicional para evitar el uso de la funcionalidad nueva en ODBC *3. x* al trabajar con controladores ODBC *2. x* . Los controladores ODBC *2. x* no admiten la funcionalidad nueva de ODBC *3. x* , solo porque la aplicación declara que sigue la especificación de ODBC *3. x* . Además, los controladores ODBC *3. x* no dejan de admitir la funcionalidad nueva de ODBC *3. x* , solo porque la aplicación declara que sigue la especificación ODBC *2. x* .
