---
title: Propiedad ProtocolName (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 753a3ddfe1e7d808380464ef5010bbe5a18ac18c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040895"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>Propiedad ProtocolName (clase ClientNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene el nombre del protocolo de red actual especificado por el [configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Un valor de cadena que especifica el nombre del cliente actual de red protocolo al que hace referencia el [método SetOrderValue (clase ClientNetworkProtocol)](https://technet.microsoft.com/library/ms179295.aspx).  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar bibliotecas de red y protocolos de red de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
