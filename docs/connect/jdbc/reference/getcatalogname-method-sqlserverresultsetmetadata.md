---
title: "Método getCatalogName (SQLServerResultSetMetaData) | Documentos de Microsoft"
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
apiname: SQLServerResultSetMetaData.getCatalogName
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 64f62569-5d8e-411f-a98d-ddc52798391e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72a03ba3b2b3d4631b25d1ade86cb6f7e959c2cb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getcatalogname-method-sqlserverresultsetmetadata"></a>Método getCatalogName (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtiene el nombre de catálogo para la tabla que incluye la columna designada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getCatalogName(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columna*  
  
 Un **int** que indica el índice de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre del catálogo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCatalogName especificado por el método getCatalogName en la interfaz java.sql.ResultSetMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros de SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
