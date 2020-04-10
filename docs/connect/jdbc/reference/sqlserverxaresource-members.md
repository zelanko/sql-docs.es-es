---
title: Miembros SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d41f89ce541d6bb6497ad0702511c303704a41b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925667"
---
# <a name="sqlserverxaresource-members"></a>Miembros de SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  En las siguientes tablas se enumeran los miembros que expone la clase [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Fields  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|Se utiliza para permitir transacciones XA estrechamente acopladas, las cuales tienen identificadores de rama de transacción XA diferentes (XID), pero tienen el mismo identificador de transacción global (GTRID).|  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|Confirma la transacción global que especifica el objeto Xid determinado.|  
|[end](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|Finaliza el trabajo realizado en nombre de una bifurcación de transacción.|  
|[forget](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|Indica al administrador de recursos que se olvide de una bifurcación de transacción completada heurísticamente.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|Obtiene el valor de tiempo de espera de la transacción actual establecido para [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|Determina si la instancia del administrador de recursos que el objeto de destino representa es igual que la instancia del administrador de recursos que el objeto determinado XAResource representa.|  
|[prepare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|Solicita que el administrador de recursos prepara para una confirmación de la transacción especificada por objeto Xid determinado.|  
|[recover](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|Obtiene una lista de bifurcaciones de transacción preparadas de un administrador de recursos.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|Solicita que el administrador de recursos revierta el trabajo realizado en nombre de una bifurcación de transacción.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|Establece el valor de tiempo de espera de transacción actual para este objeto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Comienza a funcionar en nombre de una bifurcación de transacción especificada en el objeto Xid.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>Consulte también  
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
