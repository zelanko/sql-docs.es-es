---
title: Método Recover (SQLServerXAResource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerXAResource.recover
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 840ecfcf-0dd3-4b7b-976f-dc9a96cd1464
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72efa07b757aaeab8a51646e802e8c5908a62d07
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="recover-method-sqlserverxaresource"></a>Método recover (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Obtiene una lista de bifurcaciones de transacción preparadas de un administrador de recursos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.transaction.xa.Xid[] recover(int flags)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *flags*  
  
 Un **int** valor que puede tomar uno de los siguientes valores: XAResource.TMSTARTRSCAN o XAResource.TMENDRSCAN o XAResource.TMNOFLAGS o XAResource.TMSTARTTRSCAN | XAResource.TMENDRSCAN.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Xid.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentarios  
 Este método de recuperación especificado por el método de recuperación en la interfaz javax.transaction.xa.XAResource.  
  
 Si el parámetro **marca** no es XAResource.TMSTARTRSCAN o XAResource.TMSTARTRSCAN | XAResource.TMENDRSCAN, un examen de recuperación debe estar en curso.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
