---
title: Método updateTimestamp (java.lang.String, java.sql.Timestamp) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateTimestamp (java.lang.String, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d468357-bf73-484c-9a30-3671e399cf26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 59d23bf2536806135b2ec5068c2478e30b4353a1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998151"
---
# <a name="updatetimestamp-method-javalangstring-javasqltimestamp"></a>Método updateTimestamp (java.lang.String, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor timestamp según el nombre de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateTimestamp(java.lang.String columnName,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
 *x*  
  
 Un valor timestamp.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateTimestamp especifica este método updateTimestamp en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [updateTimestamp (método) &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
