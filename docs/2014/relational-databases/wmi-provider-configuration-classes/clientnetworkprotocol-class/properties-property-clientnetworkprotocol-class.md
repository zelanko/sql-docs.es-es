---
title: Propiedad Properties (clase ClientNetworkProtocol) | Documentos de Microsoft
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4882f26e1f74fd68e67f14172482bcc674d1b06e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107142"
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
 Una matriz de [clase ClientNetworkProtocolProperty](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) objetos que representan las propiedades admitidas por el protocolo de red de cliente actual que hace referencia el `OrderValue` propiedad.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de cliente y bibliotecas de red](http://technet.microsoft.com/library/ms181035.aspx)  
  
  