---
title: Compatibilidad con columnas dispersas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e1583dad869860bdd2f555a354850c7f7a1198
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62691957"
---
# <a name="sparse-columns-support-odbc"></a>Compatibilidad con columnas dispersas (ODBC)
  En este tema se describe la compatibilidad ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con columnas dispersas. Para obtener un ejemplo que muestra la compatibilidad de ODBC con columnas dispersas, vea [llamar a SQLColumns sobre una tabla con columnas dispersas](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md). Para obtener más información sobre las columnas dispersas, vea [con las columnas dispersas en SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="statement-metadata"></a>Metadatos de instrucción  
 El campo del descriptor de parámetros de la aplicación (APD) y el atributo de instrucción SQL_SOPT_SS_NAME_SCOPE aceptan los valores adicionales SQL_SS_NAME_SCOPE_EXTENDED y SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET. Estos valores especifican qué columnas se incluyen en el conjunto de resultados devuelto por [SQLColumns](../../native-client-odbc-api/sqlcolumns.md). Para obtener más información acerca de SQL_SOPT_SS_NAME_SCOPE, vea [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
 Es posible utilizar un nuevo descriptor de filas de implementación (IRD), un campo SQLSMALLINT de solo lectura denominado SQL_CA_SS_IS_COLUMN_SET, para determinar si una columna es un valor `column_set` XML. SQL_CA_SS_IS_COLUMN_SET toma los valores SQL_TRUE y SQL_FALSE.  
  
## <a name="catalog-metadata"></a>Metadatos de catálogo  
 Se han agregado dos columnas específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SS_IS_SPARSE y SS_IS_COLUMN_SET) al conjunto de resultados de [SQLColumns](../../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="odbc-function-support-for-sparse-columns"></a>Compatibilidad de funciones ODBC con columnas dispersas  
 Las funciones ODBC que se muestran a continuación se han actualizado para admitir columnas dispersas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
