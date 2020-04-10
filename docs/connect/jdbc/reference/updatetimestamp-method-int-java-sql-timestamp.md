---
title: Método updateTimestamp (int, java.sql.Timestamp) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateTimestamp (int, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db83d9d7-137b-4a28-a2ca-d4782e0a256e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb09123dfc52c943c155fb21ef7924061c0348
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919535"
---
# <a name="updatetimestamp-method-int-javasqltimestamp"></a>Método updateTimestamp (int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor timestamp según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateTimestamp(int index,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Valor **int** que indica el índice de la columna.  
  
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
  
  
