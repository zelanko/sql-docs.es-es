---
title: "Método supportsNonNullableColumns (SQLServerDatabaseMetaData) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.supportsNonNullableColumns
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 7c32ea64-460e-4636-8a3b-07c8abeed687
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4e9e733d75bad0e732e83bd0d607e42797309e9
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="supportsnonnullablecolumns-method-sqlserverdatabasemetadata"></a>Método supportsNonNullableColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si las columnas en esta base de datos se pueden definir para que no admitan valores NULL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsNonNullableColumns()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método supportsNonNullableColumns especificado por el método supportsNonNullableColumns en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
