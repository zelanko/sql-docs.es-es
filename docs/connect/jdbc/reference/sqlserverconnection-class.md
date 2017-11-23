---
title: Clase SQLServerConnection | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 385bef4155f4b41f181774b1559282c42ac1fbee
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverconnection-class"></a>Clase SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa una conexión JDBC a una [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Comentarios  
 SQLServerConnection admite la agrupación de conexiones de JDBC y puede tener una conexión JDBC física o una conexión JDBC lógica. SQLServerConnection administra el control de transacciones para todas las instrucciones que se crearon a partir de él, y pueden participar en transacciones distribuidas XA administradas a través de un adaptador XAResource.  
  
 SQLServerConnection administra un grupo de identificadores de instrucción preparada. Las instrucciones preparadas se generan una vez y, por lo general, se ejecutan muchas veces con valores de datos diferentes para sus parámetros. Las instrucciones preparadas también se mantienen en cierres de conexiones lógicas (agrupadas).  
  
> [!NOTE]  
>  SQLServerConnection no es seguro para subprocesos. Sin embargo, se pueden procesar varias instrucciones que se crean a partir de una única conexión de forma simultánea en subprocesos que se desarrollan a la vez.  
  
 Esta clase admite la acción de desencapsular para la clase SQLServerConnection, la interfaz java.sql.connection y la interfaz de ISQLServerConnection. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
