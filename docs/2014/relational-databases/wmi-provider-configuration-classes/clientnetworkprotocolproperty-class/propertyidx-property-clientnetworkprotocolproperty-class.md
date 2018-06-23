---
title: Propiedad PropertyIdx (clase ClientNetworkProtocolProperty) | Documentos de Microsoft
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
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 42388eb8158e12f5a4458364e39bf9ce1576e70f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108047"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>Propiedad PropertyIdx (clase ClientNetworkProtocolProperty)
  Obtiene o establece el valor de índice de la propiedad de la matriz de propiedad al que hace referencia el [propiedad Properties (clase ClientNetworkProtocol)](../clientnetworkprotocol-class/clientnetworkprotocol-class.md) de la [clase ClientNetworkProtocol](../clientnetworkprotocol-class/clientnetworkprotocol-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocolProperty](clientnetworkprotocolproperty-class.md) objeto que representa un atributo de protocolo de red utilizado por el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de `uint32` que especifica el valor de índice de matriz de la propiedad actual.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  