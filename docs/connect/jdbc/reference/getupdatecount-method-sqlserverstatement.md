---
title: Método getUpdateCount (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6f05796220e305a0d6e06e15a58f780048d49a53
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790531"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>Método getUpdateCount (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el resultado actual como un recuento de actualizaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que contiene el recuento de la actualización. Si el resultado que se devuelve es un objeto de conjunto de resultados o no hay más resultados, se devolverá -1.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getUpdateCount especificado por el método getUpdateCount en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
