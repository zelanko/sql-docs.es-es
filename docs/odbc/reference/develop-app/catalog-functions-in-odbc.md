---
title: Las funciones de ODBC de catálogo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bbff6af05123484c09cbd514f626b05d438d79e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions-in-odbc"></a>Funciones de catálogo de ODBC
ODBC contiene las siguientes funciones de catálogo:  
  
|Función|Description|  
|--------------|-----------------|  
|**SQLTables**|Devuelve una lista de catálogos, esquemas, tablas o tipos de tabla del origen de datos.|  
|**SQLColumns**|Devuelve una lista de columnas en una o varias tablas.|  
|**SQLStatistics**|Devuelve una lista de las estadísticas sobre una sola tabla. También devuelve una lista de índices asociados a esa tabla.|  
|**SQLSpecialColumns**|Devuelve una lista de columnas que identifica de forma única una fila en una sola tabla. También devuelve una lista de columnas de la tabla que se actualizan automáticamente.|  
|**SQLPrimaryKeys**|Devuelve una lista de columnas que componen la clave principal de una sola tabla.|  
|**SQLForeignKeys**|Devuelve una lista de las claves externas en una única tabla o una lista de las claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLTablePrivileges**|Devuelve una lista de los privilegios asociados con una o más tablas.|  
|**SQLColumnPrivileges**|Devuelve una lista de los privilegios asociados con una o varias columnas en una sola tabla.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto y las columnas del conjunto de resultados de un único procedimiento.|  
|**SQLGetTypeInfo**|Devuelve una lista de los tipos de datos SQL admitidos por el origen de datos. Estos tipos de datos se suelen usar en **CREATE TABLE** y **ALTER TABLE** instrucciones.|  
  
 Dado que **SQLTables**, **SQLColumns**, **SQLStatistics**, y **SQLSpecialColumns** se ajustan a la CLI de grupo abierto y **SQLGetTypeInfo** se ajusta a ISO CLI 92, se implementan mediante la mayoría de los controladores. Las funciones de catálogo restantes están en el nivel de conformidad de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Vistas de esquema](../../../odbc/reference/develop-app/schema-views.md)
