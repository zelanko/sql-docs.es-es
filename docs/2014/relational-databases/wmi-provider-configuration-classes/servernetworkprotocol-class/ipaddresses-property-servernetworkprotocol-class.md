---
title: Propiedad IpAddresses (clase ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- IpAddresses Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 20979e9647d2d80f7498a5ec517d7403cd0ccf83
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150626"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>Propiedad IpAddresses (clase ServerNetworkProtocol)
  Obtiene las direcciones IP asociadas al protocolo de red del servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.IpAddresses [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un `ServerNetworkProtocol` objeto que representa el protocolo de red utilizado por la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Una matriz de [clase ServerNetworkProtocolIPAdress](../servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) objetos que representan las direcciones IP admitidas por el protocolo de red de servidor.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y las bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
