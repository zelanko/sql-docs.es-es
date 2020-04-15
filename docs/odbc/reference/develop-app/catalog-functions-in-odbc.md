---
title: Funciones de catálogo en ODBC ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6731018b99f2f3043e48ee7c174a08cb9ef71fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306236"
---
# <a name="catalog-functions-in-odbc"></a>Funciones de catálogo de ODBC
ODBC contiene las siguientes funciones de catálogo:  
  
|Función|Descripción|  
|--------------|-----------------|  
|**SQLTables**|Devuelve una lista de catálogos, esquemas, tablas o tipos de tabla en el origen de datos.|  
|**SQLColumns**|Devuelve una lista de columnas en una o varias tablas.|  
|**SQLStatistics**|Devuelve una lista de estadísticas sobre una sola tabla. También devuelve una lista de índices asociados a esa tabla.|  
|**SQLSpecialColumns**|Devuelve una lista de columnas que identifica de forma única una fila en una sola tabla. También devuelve una lista de columnas de esa tabla que se actualizan automáticamente.|  
|**SQLPrimaryKeys**|Devuelve una lista de columnas que componen la clave principal de una sola tabla.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de claves externas en otras tablas que hacen referencia a una sola tabla.|  
|**SQLTablePrivileges**|Devuelve una lista de privilegios asociados a una o varias tablas.|  
|**SQLColumnPrivileges**|Devuelve una lista de privilegios asociados a una o varias columnas en una sola tabla.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto y las columnas del conjunto de resultados de un único procedimiento.|  
|**SQLGetTypeInfo**|Devuelve una lista de los tipos de datos SQL admitidos por el origen de datos. Estos tipos de datos se utilizan generalmente en las instrucciones **CREATE TABLE** y **ALTER TABLE.**|  
  
 Dado que **SQLTables**, **SQLColumns**, **SQLStatistics**y **SQLSpecialColumns** se ajustan a la CLI de grupo abierto y **SQLGetTypeInfo** se ajusta a la CLI de ISO 92, la mayoría de los controladores los implementan. Las funciones de catálogo restantes se encuentran en el nivel de conformidad ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Vistas de esquema](../../../odbc/reference/develop-app/schema-views.md)
