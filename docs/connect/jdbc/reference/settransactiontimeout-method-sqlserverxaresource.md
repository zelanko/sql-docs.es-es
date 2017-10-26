---
title: "Método setTransactionTimeout (SQLServerXAResource) | Documentos de Microsoft"
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
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d2bcc25cfb09d40df95029f0c9d36e38e9658725
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>Método setTransactionTimeout (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor de tiempo de espera de transacción actual para este [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *segundos*  
  
 Un **int** valor.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el tiempo de espera se estableció correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentarios  
 Este método setTransactionTimeout especificado por el método setTransactionTimeout en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  

