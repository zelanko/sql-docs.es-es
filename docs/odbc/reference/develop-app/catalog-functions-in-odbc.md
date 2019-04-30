---
title: Funciones de catálogo de ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84c870d45cc487fc9ec5497e43b764bd4187d2f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217626"
---
# <a name="catalog-functions-in-odbc"></a>Funciones de catálogo de ODBC
ODBC contiene las funciones de catálogo siguientes:  
  
|Función|Descripción|  
|--------------|-----------------|  
|**SQLTables**|Devuelve una lista de catálogos, esquemas, tablas o tipos de tabla del origen de datos.|  
|**SQLColumns**|Devuelve una lista de columnas en una o varias tablas.|  
|**SQLStatistics**|Devuelve una lista de las estadísticas sobre una sola tabla. También devuelve una lista de los índices asociados a esa tabla.|  
|**SQLSpecialColumns**|Devuelve una lista de columnas que identifica de forma única una fila en una sola tabla. También devuelve una lista de columnas de esa tabla que se actualizan automáticamente.|  
|**SQLPrimaryKeys**|Devuelve una lista de columnas que componen la clave principal de una sola tabla.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de las claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLTablePrivileges**|Devuelve una lista de los privilegios asociados a una o varias tablas.|  
|**SQLColumnPrivileges**|Devuelve una lista de los privilegios asociados a una o varias columnas en una sola tabla.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto y las columnas del conjunto de resultados de un procedimiento único.|  
|**SQLGetTypeInfo**|Devuelve una lista de los tipos de datos SQL admitida por el origen de datos. Estos tipos de datos se suelen usar en **CREATE TABLE** y **ALTER TABLE** instrucciones.|  
  
 Dado que **SQLTables**, **SQLColumns**, **SQLStatistics**, y **SQLSpecialColumns** se ajustan a la CLI de grupo abierto y **SQLGetTypeInfo** se ajusta a la imagen ISO CLI 92, se implementan mediante la mayoría de los controladores. Las funciones de catálogo restantes están en el nivel de conformidad de ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Vistas de esquema](../../../odbc/reference/develop-app/schema-views.md)
