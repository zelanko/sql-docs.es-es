---
title: Compatibilidad con columnas dispersas (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2b294c0b1226722f98a14f1f49aeb077216a18d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200868"
---
# <a name="sparse-columns-support-odbc"></a>Compatibilidad con columnas dispersas (ODBC)
  En este tema se describe la compatibilidad ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con columnas dispersas. Para obtener un ejemplo que muestra la compatibilidad de ODBC con columnas dispersas, vea [llamar a SQLColumns sobre una tabla con columnas dispersas](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md). Para obtener más información sobre las columnas dispersas, vea [Sparse Columns Support in SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="statement-metadata"></a>Metadatos de instrucción  
 El campo del descriptor de parámetros de la aplicación (APD) y el atributo de instrucción SQL_SOPT_SS_NAME_SCOPE aceptan los valores adicionales SQL_SS_NAME_SCOPE_EXTENDED y SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET. Estos valores especifican qué columnas se incluyen en el conjunto de resultados devuelto por [SQLColumns](../../native-client-odbc-api/sqlcolumns.md). Para obtener más información sobre SQL_SOPT_SS_NAME_SCOPE, vea [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
 Es posible utilizar un nuevo descriptor de filas de implementación (IRD), un campo SQLSMALLINT de solo lectura denominado SQL_CA_SS_IS_COLUMN_SET, para determinar si una columna es un valor `column_set` XML. SQL_CA_SS_IS_COLUMN_SET toma los valores SQL_TRUE y SQL_FALSE.  
  
## <a name="catalog-metadata"></a>Metadatos de catálogo  
 Dos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] columnas específicas (SS_IS_SPARSE y SS_IS_COLUMN_SET) se han agregado al conjunto de resultados para [SQLColumns](../../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="odbc-function-support-for-sparse-columns"></a>Compatibilidad de funciones ODBC con columnas dispersas  
 Las funciones ODBC que se muestran a continuación se han actualizado para admitir columnas dispersas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  