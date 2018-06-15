---
title: Commit (método) (SQLServerXAResource) | Documentos de Microsoft
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
- SQLServerXAResource.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d0f8612-fb4a-4eca-bc37-8342e1419fd4
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c6bdb28d36a148cab744fe5d9b0dbe321998757
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32830876"
---
# <a name="commit-method-sqlserverxaresource"></a>Método commit (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Confirma la transacción global que se especifica el objeto Xid determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void commit(javax.transaction.xa.Xid xid,  
                   boolean onePhase)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *XID*  
  
 Un objeto Xid.  
  
 *onePhase*  
  
 A **booleano** valor.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentarios  
 Este método de confirmación es especificado por el método commit en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
