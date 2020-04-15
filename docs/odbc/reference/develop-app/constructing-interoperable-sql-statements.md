---
title: Construyendo instrucciones SQL interoperables Microsoft Docs
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
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282528"
---
# <a name="constructing-interoperable-sql-statements"></a>Crear instrucciones SQL Interoperable
Como se mencionó en las secciones anteriores, las aplicaciones interoperables deben usar la gramática SQL ODBC. Sin embargo, más allá de utilizar esta gramática, se enfrentan a una serie de problemas adicionales por aplicaciones interoperables. Por ejemplo, ¿qué hace una aplicación si desea utilizar una característica, como combinaciones externas, que no es compatible con todos los orígenes de datos?  
  
 En este punto, el escritor de aplicaciones debe tomar algunas decisiones sobre qué características de lenguaje son necesarias y cuáles son opcionales. En la mayoría de los casos, si un controlador determinado no admite una característica requerida por la aplicación, la aplicación simplemente se niega a ejecutarse con ese controlador. Sin embargo, si la característica es opcional, la aplicación puede evitar la característica. Por ejemplo, podría deshabilitar las partes de la interfaz que permiten al usuario utilizar la característica.  
  
 Para determinar qué características se admiten, las aplicaciones comienzan llamando a **SQLGetInfo** con la opción SQL_SQL_CONFORMANCE. El nivel de conformidad de SQL proporciona a la aplicación una vista amplia de qué SQL se admite. Para refinar esta vista, la aplicación llama a **SQLGetInfo** con cualquiera de varias otras opciones. Para obtener una lista completa de estas opciones, vea la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md) Por último, **SQLGetTypeInfo** devuelve información sobre los tipos de datos admitidos por el origen de datos. En las secciones siguientes se enumeran una serie de posibles factores que las aplicaciones deben tener en cuenta al construir instrucciones SQL interoperables.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de esquema y catálogo](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posición del catálogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Caso de identificador](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Secuencias de escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Literales prefijos y sufijos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcadores de parámetros en las llamadas a procedimiento](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Instrucciones DDL](../../../odbc/reference/develop-app/ddl-statements.md)
