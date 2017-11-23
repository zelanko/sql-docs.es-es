---
title: "Método GetNextOrderValue (clase ClientNetworkProtocol) | Documentos de Microsoft"
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
apiname: GetNextOrderValue Method (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: GetNextOrderValue method
ms.assetid: d741dc5c-c225-43d9-a730-7ad664ac525f
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 912009a7092b897610751e11a625ae122c34cbde
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="getnextordervalue-method-clientnetworkprotocol-class"></a>Método GetNextOrderValue (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Selecciona el protocolo que se encuentra en la siguiente posición en la lista de protocolos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.GetNextOrderValue()  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 A [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)   
 [Configurar protocolos de red de cliente y bibliotecas de red](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
