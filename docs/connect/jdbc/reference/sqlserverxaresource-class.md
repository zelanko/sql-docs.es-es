---
title: Clase SQLServerXAResource | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46281eca1f326f39a0e8aff7e167214152a839e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32847798"
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
  
  
