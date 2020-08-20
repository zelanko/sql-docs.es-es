---
description: Funciones de catálogo de ODBC
title: Funciones de catálogo en ODBC | Microsoft Docs
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
ms.openlocfilehash: b7a34a29e55f6705ccc98e5644096ac6ea7bfd67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465977"
---
# <a name="catalog-functions-in-odbc"></a>Funciones de catálogo de ODBC
ODBC contiene las siguientes funciones de catálogo:  
  
|Función|Descripción|  
|--------------|-----------------|  
|**SQLTables**|Devuelve una lista de catálogos, esquemas, tablas o tipos de tabla en el origen de datos.|  
|**SQLColumns**|Devuelve una lista de columnas de una o varias tablas.|  
|**SQLStatistics**|Devuelve una lista de estadísticas sobre una sola tabla. También devuelve una lista de índices asociados a esa tabla.|  
|**SQLSpecialColumns**|Devuelve una lista de las columnas que identifican de forma única una fila en una sola tabla. También devuelve una lista de las columnas de la tabla que se actualizan automáticamente.|  
|**SQLPrimaryKeys**|Devuelve una lista de columnas que componen la clave principal de una sola tabla.|  
|**SQLForeignKeys**|Devuelve una lista de claves externas en una sola tabla o una lista de claves externas de otras tablas que hacen referencia a una sola tabla.|  
|**SQLTablePrivileges**|Devuelve una lista de privilegios asociados a una o más tablas.|  
|**SQLColumnPrivileges**|Devuelve una lista de privilegios asociados a una o más columnas de una sola tabla.|  
|**SQLProcedures**|Devuelve una lista de procedimientos en el origen de datos.|  
|**SQLProcedureColumns**|Devuelve una lista de parámetros de entrada y salida, el valor devuelto y las columnas del conjunto de resultados de un único procedimiento.|  
|**SQLGetTypeInfo**|Devuelve una lista de los tipos de datos de SQL admitidos por el origen de datos. Estos tipos de datos se utilizan generalmente en las instrucciones **CREATE TABLE** y **ALTER TABLE** .|  
  
 Como **SQLTables**, **SQLColumns**, **SQLStatistics**y **SQLSpecialColumns** se ajustan a la CLI de Open Group y **SQLGetTypeInfo** se ajusta a la CLI ISO 92, se implementan en la mayoría de los controladores. Las funciones de catálogo restantes se encuentran en el nivel de conformidad con ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Vistas de esquema](../../../odbc/reference/develop-app/schema-views.md)
