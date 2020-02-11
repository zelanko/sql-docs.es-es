---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 737ace72f201f3abe192393b1a1cc3747f5774e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067761"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges** devuelve SQL_SUCCESS si existen o no valores para los parámetros*nombrecatálogo*, *SchemaName*, *TableName*o *columnName* . **SQLFetch** devuelve SQL_NO_DATA cuando se usan valores no válidos en estos parámetros.  
  
 **SQLColumnPrivileges** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLColumnPrivileges** en un cursor actualizable (dinámico o de conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>Consulte también  
 [SQLColumnPrivileges función)](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
