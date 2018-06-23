---
title: Propiedad NumberOfFlags (clase ClientNetworkProtocol) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0e2d483fc4916be6175093cd68470a57819544ae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202883"
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
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  