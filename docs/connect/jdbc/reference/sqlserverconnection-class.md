---
title: Clase SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7e09c80081dc4e3c9230cfba51b1b477420146fb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67971742"
---
# <a name="sqlserverconnection-class"></a>Clase SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa una conexión JDBC a una base de datos de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md), java.io.Serializable  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>Observaciones  
 SQLServerConnection admite la agrupación de conexiones de JDBC y puede ser una conexión JDBC física o una conexión lógica de JDBC. SQLServerConnection administra el control de transacciones para todas las instrucciones que se crearon a partir de él y puede participar en transacciones distribuidas XA administradas a través de un adaptador de XAResource.  
  
 SQLServerConnection administra un grupo de identificadores de instrucciones preparados. Las instrucciones preparadas se generan una vez y, por lo general, se ejecutan muchas veces con valores de datos diferentes para sus parámetros. Las instrucciones preparadas también se mantienen en cierres de conexiones lógicas (agrupadas).  
  
> [!NOTE]  
>  SQLServerConnection no es segura para los subprocesos. Sin embargo, se pueden procesar varias instrucciones que se crean a partir de una única conexión de forma simultánea en subprocesos que se desarrollan a la vez.  
  
 Esta clase admite la desencapsulación en la clase SQLServerConnection, la interfaz java.sql.connection y la interfaz ISQLServerConnection. Para más información, consulte [Contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
