---
title: Propiedad PropertyIdx (clase ClientNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b8a088c5a02f010bda32da9b67b962e5445c02ab
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51214741"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>Propiedad PropertyIdx (clase ClientNetworkProtocolProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene o establece el valor de índice de la propiedad en la matriz de propiedades al que hace referencia el [propiedad Properties (clase ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md) de la [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un [clase ClientNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) objeto que representa un atributo del protocolo de red utilizado por el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Un **uint32** valor que especifica el valor de índice de matriz de la propiedad actual.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
