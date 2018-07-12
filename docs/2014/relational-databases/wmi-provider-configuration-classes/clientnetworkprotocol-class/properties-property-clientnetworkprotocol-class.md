---
title: Propiedad Properties (clase ClientNetworkProtocol) | Microsoft Docs
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
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 569c1b0f8f140bd05c2be03286e6c9fa1d66a200
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202735"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Propiedad Properties (clase ClientNetworkProtocol)
  Obtiene las propiedades asociadas al protocolo de red del cliente actual especificado por [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Una matriz de [clase ClientNetworkProtocolProperty](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) objetos que representan las propiedades admitidas por el protocolo de red de cliente actual al que hace referencia el `OrderValue` propiedad.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar bibliotecas de red y protocolos de red de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
