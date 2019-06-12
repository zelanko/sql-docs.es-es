---
title: Método rowInserted (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowInserted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e7c10372-0be8-4baa-87f7-ed6b66003357
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: da746533231983d67bbfe3689d0df63086d678bc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765379"
---
# <a name="rowinserted-method-sqlserverresultset"></a>Método rowInserted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si la fila actual ha tenido una inserción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowInserted()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si ha habido una inserción en una fila y si se detectan inserciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método rowUpdated especificado por el método rowUpdated en la interfaz java.sql.ResultSet.  
  
 El valor que se devuelve depende de si este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) puede detectar inserciones visibles.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no detecta las filas insertadas para cualquier tipo de cursor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
