---
title: Método rollback (SQLServerXAResource) | Microsoft Docs
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
ms.openlocfilehash: 4245dc4314d955aefc3538a38dcd2192403fed9a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975727"
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
  
 Objeto XID.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Notas  
 El método rollback especifica este método rollback en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
