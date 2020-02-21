---
title: Método commit (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d0f8612-fb4a-4eca-bc37-8342e1419fd4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85bc4f123dd29025e906d57d64f21746df5f2e07
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67955556"
---
# <a name="commit-method-sqlserverxaresource"></a>Método commit (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Confirma la transacción global que determina el objeto Xid especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void commit(javax.transaction.xa.Xid xid,  
                   boolean onePhase)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *xid*  
  
 Un objeto Xid.  
  
 *onePhase*  
  
 Un valor **boolean**.  
  
## <a name="exceptions"></a>Excepciones  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Observaciones  
 El método de confirmación especifica este método de confirmación en la interfaz javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
