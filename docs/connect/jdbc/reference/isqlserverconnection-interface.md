---
title: Interfaz de ISQLServerConnection | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8049bb3024fc642a1c6338608ead03d98f781fd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="isqlserverconnection-interface"></a>Interfaz de ISQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa una conexión JDBC a una [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos. Esta interfaz se agregó en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.sql.Connection  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>Comentarios  
 Esta interfaz se implementa mediante [clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Esta interfaz expone los siguientes [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-campo específico:  
  
|Campo|Para obtener más información, vea|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

