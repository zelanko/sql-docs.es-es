---
title: Método SetFlag (clase ClientNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetFlag Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetFlag method
ms.assetid: 0407520f-2f84-4f68-b2b7-429697286c1b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6c33eca0bf3281243aeee42ed89001cf9108d5d4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245091"
---
# <a name="setflag-method-clientnetworkprotocolproperty-class"></a>Método SetFlag (clase ClientNetworkProtocolProperty)
  Establece la marca de la propiedad actual a la que hace referencia el valor de la [propiedad PropertyIdx (clase ClientNetworkProtocolProperty)](clientnetworkprotocolproperty-class.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetFlag(  
BoolValue  
) [=]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ClientNetworkProtocolProperty](clientnetworkprotocolproperty-class.md) que representa un atributo del Protocolo de red utilizado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] el cliente.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*BoolValue*|Valor booleano que especifica el nuevo valor de la marca.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
