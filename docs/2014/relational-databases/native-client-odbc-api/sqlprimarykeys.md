---
title: SQLPrimaryKeys | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cb0dc440025730c278206a751a5ce741b69b0f6e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105616"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Una tabla puede tener una o varias columnas que pueden actuar como identificadores de fila únicos y tablas creadas sin una restricción PRIMARY KEY devuelven un conjunto a SQLPrimaryKeys de resultados vacío. La función ODBC [SQLSpecialColumns](sqlspecialcolumns.md) candidatos para las tablas sin claves principales del identificador de fila de informes.  
  
 SQLPrimaryKeys devuelve SQL_SUCCESS si existen o no valores para *CatalogName*, *SchemaName*, o *TableName* parámetros. SQLFetch devuelve SQL_NO_DATA cuando se usan valores no válidos en estos parámetros.  
  
 SQLPrimaryKeys se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar SQLPrimaryKeys en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, que indica que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el *CatalogName* parámetro: *nombre_servidor_vinculado.nombre_catálogo*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys y parámetros con valores de tabla  
 Si el atributo de instrucción SQL_SOPT_SS_NAME_SCOPE tiene el valor SQL_SS_NAME_SCOPE_TABLE_TYPE, en lugar de su valor predeterminado de SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys devolverá información sobre las columnas de clave principal de tipos de tabla. Para obtener más información sobre SQL_SOPT_SS_NAME_SCOPE, vea [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLPrimaryKeys, función](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  