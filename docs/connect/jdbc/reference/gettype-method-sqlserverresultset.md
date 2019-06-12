---
title: Método getType (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffbc4a02-e851-431c-bc1a-7ab381d982bb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 38cc11c791666ebefadf71a412ea5a5858c03f34
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786152"
---
# <a name="gettype-method-sqlserverresultset"></a>Método getType (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el tipo de cursor de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getType()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el tipo de cursor actual, que puede ser uno de los siguientes valores:  
  
 ResultSet.TYPE_FORWARD_ONLY  
  
 ResultSet.TYPE_SCROLL_INSENSITIVE  
  
 ResultSet.TYPE_SCROLL_SENSITIVE  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getTime especifica este método getTime en la interfaz java.sql.ResultSet.  
  
 Este método se puede utilizar para determinar el tipo de cursor actual. Si la aplicación seleccionara TYPE_FORWARD_ONLY o utilizase un tipo de cursor predeterminado, se devolverá TYPE_FORWARD_ONLY.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
