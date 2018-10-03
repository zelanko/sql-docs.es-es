---
title: Propiedad ProtocolDLL (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- ProtocolDLL Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: fe8650d5-7b9d-46f8-bf74-baf1d9d2a06a
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 67fdda95d3a447f9390b8366f99a97e269c99ddd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115645"
---
# <a name="protocoldll-property-clientnetworkprotocol-class"></a>Propiedad ProtocolDLL (clase ClientNetworkProtocol)
  Obtiene el nombre del archivo .dll que necesita el protocolo de red especificado por [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de cadena que especifica el archivo .dll de protocolo requerido por el protocolo de red del cliente.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar bibliotecas de red y protocolos de red de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
