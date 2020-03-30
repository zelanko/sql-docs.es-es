---
title: Método getPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8f2cf03eb2eeaa3bb742a1f0d665c360e0d5f74
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981039"
---
# <a name="getpacketsize-method-sqlserverdatasource"></a>Método getPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el tamaño del paquete de red actual que se usa para establecer la comunicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y se especifica en bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Valor de tipo **int** que contiene el tamaño del paquete de red actual.  
  
## <a name="remarks"></a>Observaciones  
 Si no se establece la propiedad packetSize, el método getPacketSize devuelve el valor predeterminado 8000.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
