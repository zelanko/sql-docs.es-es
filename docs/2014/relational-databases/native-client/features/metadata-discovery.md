---
title: Detección de metadatos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d26329d11885061b01e6147f145ce42a2a8855b
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395358"
---
# <a name="metadata-discovery"></a>Detección de metadatos
  La mejora de la detección de metadatos en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las aplicaciones cliente nativas para asegurarse de que esos metadatos de columna o parámetro devuelto de la ejecución de una consulta están compatible con los metadatos o idéntico al formato especificado antes de ejecuta la consulta. Se producirá un error si los metadatos devueltos tras la ejecución de la consulta no son compatibles con el formato de los metadatos especificados antes de la ejecución de la consulta.  
  
 En el caso de las funciones bcp y ODBC y las interfaces IBCPSession e IBCPSession2, ahora se puede especificar una lectura diferida (detección de metadatos diferida) para evitar la detección de metadatos en operaciones de salida de consulta. De este modo, mejora el rendimiento y se eliminan los errores de detección de metadatos.  
  
 Si desarrolla una aplicación utilizando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] pero se conecta a una versión de servidor anterior a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], funcionalidad se corresponderá con la versión del servidor de detección de metadatos.  
  
## <a name="remarks"></a>Notas  
 Las funciones bcp siguientes se han perfeccionado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para proporcionar una detección de metadatos mejorada:  
  
-   [bcp_columns](../../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 También verá una mejora del rendimiento cuando se especifica el formato de metadatos utilizando [bcp_setbulkmode](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md).  
  
 [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) tiene un nuevo *eOption* para controlar el comportamiento de bcp_readfmt: `BCPDELAYREADFMT`.  
  
 Las funciones ODBC siguientes se han perfeccionado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para proporcionar una detección de metadatos mejorada:  
  
-   [SQLNumResultCols](../../native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)  
  
 Las funciones miembro de OLE DB siguientes se han perfeccionado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para proporcionar una detección de metadatos mejorada:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: GetParameterInfo (consulte [ICommandWithParameters](../../native-client-ole-db-interfaces/icommandwithparameters.md) para obtener más información)  
  
 También percibirá una mejora del rendimiento si especifica el formato de metadatos mediante IBCPSession::BCPSetBulkMode.  
  
 La detección del metadatos mejorada en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es posible debido a la unión de dos procedimientos almacenados de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
