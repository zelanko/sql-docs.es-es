---
title: Método getConnection (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.getConnection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 05bdb61f-26e8-480f-a1c1-1e46a8ed4b70
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aad1cac0f8d627350ad3a4eab5730509148e8ffb
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923368"
---
# <a name="getconnection-method-sqlserverpooledconnection"></a>Método getConnection (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Crea un controlador de objeto para la conexión física que representa este objeto [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Connection.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Observaciones  
 El método getConnection especifica este método getConnection en la javax.sql.PooledConnection.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [Miembros SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [Clase SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
