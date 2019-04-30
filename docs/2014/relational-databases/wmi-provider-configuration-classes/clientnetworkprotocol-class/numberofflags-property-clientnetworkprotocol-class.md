---
title: Propiedad NumberOfFlags (clase ClientNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- NumberOfFlags Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: 7a656644-2154-419f-9787-99877f597770
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9a47f6e17a85fdf9cec169a611b9fe205ba02543
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192035"
---
# <a name="numberofflags-property-clientnetworkprotocol-class"></a>Propiedad NumberOfFlags (clase ClientNetworkProtocol)
  Obtiene el número de opciones de marca necesarias para el protocolo de red de cliente especificado por el [método SetOrderValue (clase ClientNetworkProtocol)](clientnetworkprotocol-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.NumberofFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `Uint32` que especifica el número de opciones de marca necesarias para el protocolo de red del cliente al que hace referencia la propiedad `OrderValue`.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
