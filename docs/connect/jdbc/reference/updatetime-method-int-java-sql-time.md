---
title: Método updateTime (int, java.sql.Time) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateTime (int, java.sql.Time)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa7a3ca5-1111-4480-97ca-65b632aa1e5b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43256aa2725a56286ce083b613092421bdd15274
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809953"
---
# <a name="updatetime-method-int-javasqltime"></a>Método updateTime (int, java.sql.Time)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de hora según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateTime(int index,  
                       java.sql.Time x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Un valor de hora.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateTime especificado por el método updateTime en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Ver también  
 [Método updateTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
