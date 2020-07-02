---
title: Propiedad NumberOfProps (ClientNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfProps Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfProps property
ms.assetid: 9c508bc5-c7a4-4db1-b3bf-c7098c66435a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2184904e7de2fe30afc50cf7a76e575baafb1de8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731445"
---
# <a name="numberofprops-property-clientnetworkprotocol-class"></a>Propiedad NumberOfProps (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene el número de propiedades del Protocolo de red del cliente especificado por el [método SetOrderValue (clase ClientNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.NumberOfProps [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica el número de propiedades del protocolo de red del cliente.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
