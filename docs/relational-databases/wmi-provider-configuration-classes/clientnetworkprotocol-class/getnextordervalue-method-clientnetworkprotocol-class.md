---
title: Método GetNextOrderValue (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetNextOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetNextOrderValue method
ms.assetid: d741dc5c-c225-43d9-a730-7ad664ac525f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 46f4454c3d8d3391a420e63fbe84bf1f9cf5f155
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51215013"
---
# <a name="getnextordervalue-method-clientnetworkprotocol-class"></a>Método GetNextOrderValue (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Selecciona el protocolo que se encuentra en la posición siguiente en la lista de protocolos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.GetNextOrderValue()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)   
 [Configurar bibliotecas de red y protocolos de red de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
