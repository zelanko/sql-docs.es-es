---
title: Propiedad MultiIpConfigurationSupport (clase ServerNetworkProtocol) | Microsoft Docs
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
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c4f7ba582aa5a95abacf4c653fadbba22b51b410
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179602"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>Propiedad MultiIpConfigurationSupport (clase ServerNetworkProtocol)
  Obtiene la propiedad booleana que especifica si un protocolo de red del servidor admite varias direcciones IP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un [propiedad ProtocolName (clase ServerNetworkProtocol)](servernetworkprotocol-class.md) objeto que representa el protocolo de red utilizado por la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor booleano que especifica si el protocolo de red del servidor admite varias direcciones IP: `true` si el protocolo de red del servidor admite varias direcciones IP; en caso contrario, `false`.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y las bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
