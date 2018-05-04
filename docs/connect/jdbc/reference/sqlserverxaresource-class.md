---
title: Clase SQLServerXAResource | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc12b2f49633b00addeec742104d5e525c578f0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
  
