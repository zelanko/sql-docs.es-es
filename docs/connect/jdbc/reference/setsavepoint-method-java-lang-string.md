---
description: Método setSavepoint (java.lang.String)
title: Método setSavepoint (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setSavepoint (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1cf15ec4-d9d9-4ab3-bfee-2ea43ff609a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57ed08c322b8579b92165306397fb26312d95fa3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458429"
---
# <a name="setsavepoint-method-javalangstring"></a>Método setSavepoint (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un punto de retorno con el nombre determinado en la transacción actual y devuelve el nuevo objeto [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) que lo representa.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Savepoint setSavepoint(java.lang.String sName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sName*  
  
 Un valor **String** que contiene el nombre del punto de retorno.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto SavePoint.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setSavePoint especifica este método setSavePoint en la interfaz java.sql.Connection.  
  
 El argumento *sName* se elude automáticamente mediante [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Método setSavepoint &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
