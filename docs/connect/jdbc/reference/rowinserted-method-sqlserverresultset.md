---
title: "rowInserted (método) (SQLServerResultSet) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 885d101c9f19cd416fa85155be74aabd72bdefff
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="rowinserted-method-sqlserverresultset"></a>rowInserted (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si la fila actual ha tenido una inserción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si una fila ha tenido una inserción y se detectan las inserciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método rowUpdated es especificado por el método rowUpdated en la interfaz java.sql.ResultSet.  
  
 El valor devuelto depende de si esto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto puede detectar inserciones visibles.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]no detecta las filas insertadas para cualquier tipo de cursor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
