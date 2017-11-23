---
title: "Método setDateTimeOffset (SQLServerPreparedStatement) | Documentos de Microsoft"
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
ms.assetid: 5014dba9-1755-4769-b070-6cbeecee864e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b5694a1ca12a5c6d230b2628486211b46fbd6fa
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setdatetimeoffset-method-sqlserverpreparedstatement"></a>Método setDateTimeOffset (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0.  
  
 Establece el valor de la columna especificada en el [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setDateTimeOffset(int n, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 El ordinal basado en cero de una columna.  
  
 *x*  
  
 El [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
