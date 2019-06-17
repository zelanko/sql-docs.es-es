---
title: Crear instrucciones SQL Interoperable | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc8072a6d7291a546f0f12256aa4b336da037a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63281088"
---
# <a name="constructing-interoperable-sql-statements"></a>Crear instrucciones SQL Interoperable
Como se mencionó en las secciones anteriores, las aplicaciones interoperables deben usar la gramática de SQL de ODBC. Sin embargo, mediante el uso de esta gramática, un número de problemas adicionales se enfrenta las aplicaciones interoperables. Por ejemplo, ¿qué hace una aplicación si quiere usar una característica, como las combinaciones externas, que no es compatible con todos los orígenes de datos?  
  
 En este momento, el autor de la aplicación debe tomar algunas decisiones sobre qué características de lenguaje son obligatorios y cuáles son opcionales. En la mayoría de los casos, si un controlador en particular no admite una característica necesaria para la aplicación, la aplicación simplemente rechaza ejecutar con ese controlador. Sin embargo, si la característica es opcional, la aplicación puede funcionar en torno a la característica. Por ejemplo, pueden deshabilitar aquellas partes de la interfaz que permiten al usuario usar la característica.  
  
 Para determinar qué características son compatibles, las aplicaciones se inician mediante una llamada a **SQLGetInfo** con la opción SQL_SQL_CONFORMANCE. El nivel de conformidad de SQL ofrece a la aplicación una visión amplia de las cuales SQL es compatible. Para refinar esta vista, la aplicación llama a **SQLGetInfo** con cualquier número de otras opciones. Para obtener una lista completa de estas opciones, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función. Por último, **SQLGetTypeInfo** devuelve información acerca de los tipos de datos admitidos por el origen de datos. Las siguientes secciones enumeran una serie de factores posibles que deben vigilar aplicaciones al construir instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de esquema y catálogo](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posición del catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso de identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Secuencias de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Literales prefijos y sufijos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parámetros en las llamadas a procedimiento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md)
