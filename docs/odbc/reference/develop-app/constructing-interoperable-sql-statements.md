---
description: Crear instrucciones SQL Interoperable
title: Construir instrucciones SQL interoperables | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acdb0f360242c4c9953804cb768214b0a78251dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465887"
---
# <a name="constructing-interoperable-sql-statements"></a>Crear instrucciones SQL Interoperable
Como se mencionó en las secciones anteriores, las aplicaciones interoperables deben usar la gramática de SQL de ODBC. Sin embargo, además de utilizar esta gramática, las aplicaciones interoperables pueden enfrentarse a una serie de problemas adicionales. Por ejemplo, ¿qué hace una aplicación si quiere usar una característica, como combinaciones externas, que no es compatible con todos los orígenes de datos?  
  
 En este momento, el escritor de la aplicación debe tomar algunas decisiones sobre qué características del lenguaje son necesarias y cuáles son opcionales. En la mayoría de los casos, si un controlador determinado no es compatible con una característica requerida por la aplicación, la aplicación simplemente se niega a ejecutar con ese controlador. Sin embargo, si la característica es opcional, la aplicación puede funcionar en torno a la característica. Por ejemplo, podría deshabilitar las partes de la interfaz que permiten al usuario utilizar la característica.  
  
 Para determinar qué características se admiten, las aplicaciones se inician llamando a **SQLGetInfo** con la opción SQL_SQL_CONFORMANCE. El nivel de conformidad de SQL proporciona a la aplicación una vista amplia de la compatibilidad con SQL. Para depurar esta vista, la aplicación llama a **SQLGetInfo** con cualquiera de las otras opciones. Para obtener una lista completa de estas opciones, vea la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) . Por último, **SQLGetTypeInfo** devuelve información acerca de los tipos de datos admitidos por el origen de datos. En las secciones siguientes se enumeran varios factores posibles que las aplicaciones deben ver al construir instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de esquema y catálogo](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posición del catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso de identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Secuencias de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Literales prefijos y sufijos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parámetros en las llamadas a procedimiento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md)
