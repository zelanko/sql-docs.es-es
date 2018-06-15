---
title: Método End (SQLServerXAResource) | Documentos de Microsoft
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
- SQLServerXAResource.end
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e6418b27-793b-4b36-8dfb-756aec7bcbba
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a6896afefcfc25e349338b333626a0d0f8bac16
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829830"
---
# <a name="end-method-sqlserverxaresource"></a>Método end (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Finaliza el trabajo realizado en nombre de una bifurcación de transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void end(javax.transaction.xa.Xid xid,  
                int flags)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *XID*  
  
 Un objeto Xid.  
  
 *flags*  
  
 Un **int** valor.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentarios  
 Este método final es especificado por el método end en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
