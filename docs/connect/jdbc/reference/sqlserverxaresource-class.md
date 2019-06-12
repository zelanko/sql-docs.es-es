---
title: Clase SQLServerXAResource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8cde4f1b80ae1167ba7f99c80505e3b838890113
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768349"
---
# <a name="sqlserverxaresource-class"></a>Clase SQLServerXAResource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa un XAResource para la administración de transacciones distribuidas XA.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.lang.Object  
  
 **Implementa:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Notas  
 Las transacciones XA se implementan en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el Coordinador de transacciones distribuidas (DTC) de [!INCLUDE[msCoName](../../../includes/msconame_md.md)]. La clase SQLServerXAResource efectúa llamadas a un archivo extendido dll de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] denominado sqljdbc_xa.dll, que se interrelaciona con DTC. Las llamadas XA que SQLServerXAResource recibe (XA_START, XA_END, XA_PREPARE, etc.) están asignadas a las llamadas correspondientes a las funciones DTC.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
