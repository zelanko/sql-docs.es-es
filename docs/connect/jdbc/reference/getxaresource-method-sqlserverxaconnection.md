---
title: Método getXAResource (SQLServerXAConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3d4b2132c3bbcf5612faa5f319a5358f158e2b7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977980"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>Método getXAResource (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) que utilizará el administrador de transacciones para administrar la participación de este objeto [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) en una transacción distribuida.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto XAResource.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método getXAResource especifica este método getXAResource en la interfaz javax.sql.XAConnection.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [Miembros SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [Clase SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
