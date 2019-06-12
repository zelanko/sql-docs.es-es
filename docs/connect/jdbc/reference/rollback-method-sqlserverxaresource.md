---
title: Método Rollback (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.rollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93d9d7e6-54b6-4d86-8f8c-386c6057e85e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cc8d0b925c1ae7bf1a4775fd50862647eb2a84ac
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765385"
---
# <a name="rollback-method-sqlserverxaresource"></a>Método rollback (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Solicita que el administrador de recursos revierta el trabajo realizado en nombre de una bifurcación de transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void rollback(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *xid*  
  
 Un objeto Xid.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Notas  
 El método rollback especifica este método rollback en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
