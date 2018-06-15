---
title: rowInserted (método) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca82265b8fde94c29495c529928087a20ddc5544
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32842030"
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
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no detecta las filas insertadas para cualquier tipo de cursor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
