---
title: Propiedad ProtocolOrder (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8bccb7109972dea4697e9e289081cbf47d2f9492
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065599"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>Propiedad ProtocolOrder (clase ClientNetworkProtocol)
  Obtiene el número de orden del protocolo de red del cliente al que se hace referencia actualmente especificado por el [método SetOrderValue (clase ClientNetworkProtocol)](clientnetworkprotocol-class.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que especifica el número de orden del protocolo de red del cliente al que se hace referencia actualmente establecido por el método `OrderValue`. Si el protocolo de red del cliente está deshabilitado, este valor será cero.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)   
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
