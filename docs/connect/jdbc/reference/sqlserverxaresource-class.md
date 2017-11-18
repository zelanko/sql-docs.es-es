---
title: Clase SQLServerXAResource | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c5e0cb02544e0ea96c29758f7c50179de48cf7a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxaresource-class"></a>Clase SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa un XAResource XA administración de transacciones distribuidas.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.lang.Object  
  
 **Implementa:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Comentarios  
 Las transacciones XA se implementan en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] utilizando [!INCLUDE[msCoName](../../../includes/msconame_md.md)] el Administrador de transacciones distribuidas (DTC). La clase SQLServerXAResource realiza llamadas a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] extendido dll denominado sqljdbc_xa.dll, que se interrelaciona con DTC. Las llamadas XA que reciben SQLServerXAResource (XA_START, XA_END, XA_PREPARE etc.) se asignan a las llamadas correspondientes a las funciones DTC.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

