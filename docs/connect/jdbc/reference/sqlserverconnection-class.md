---
title: Clase SQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4746e09839e2015e4b7b14963ae698c66066ac78
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783952"
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
  
## <a name="remarks"></a>Notas  
 SQLServerConnection admite la agrupación de conexiones de JDBC y puede ser una conexión JDBC física o una conexión lógica de JDBC. SQLServerConnection administra el control de transacciones para todas las instrucciones que se crearon a partir de él y puede participar en transacciones distribuidas XA administradas a través de un adaptador de XAResource.  
  
 SQLServerConnection administra un grupo de identificadores de instrucción preparada. Las instrucciones preparadas se generan una vez y, por lo general, se ejecutan muchas veces con valores de datos diferentes para sus parámetros. Las instrucciones preparadas también se mantienen en cierres de conexiones lógicas (agrupadas).  
  
> [!NOTE]  
>  SQLServerConnection no es seguro para subprocesos. Sin embargo, se pueden procesar varias instrucciones que se crean a partir de una única conexión de forma simultánea en subprocesos que se desarrollan a la vez.  
  
 Esta clase admite la acción de desencapsular para la interfaz de ISQLServerConnection, interfaz java.sql.connection y clase SQLServerConnection. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
