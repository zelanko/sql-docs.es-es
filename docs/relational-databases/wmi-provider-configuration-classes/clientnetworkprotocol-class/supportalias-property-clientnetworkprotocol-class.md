---
title: Propiedad SupportAlias (clase ClientNetworkProtocol) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SupportAlias Property (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f83e28362866b3a622b0e15670445d4e88878013
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>Propiedad SupportAlias (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Obtiene la propiedad booleana que especifica si este protocolo de red especificado por el [método SetOrderValue (clase ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md) admite alias.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SupportAlias [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad/Valor devuelto  
 Valor booleano que especifica si el protocolo de red del cliente admite alias.  
  
 Si es True, el protocolo de red del cliente admite alias.  
  
 Si es False, el protocolo de red del cliente no admite alias.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
