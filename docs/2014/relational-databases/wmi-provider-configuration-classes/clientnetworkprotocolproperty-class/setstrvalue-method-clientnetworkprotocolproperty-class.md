---
title: Método SetStrValue (clase ClientNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- SetStrValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d18fd2b716e46e08d84a966677b4e76b28fc9a88
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055955"
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>Método SetStrValue (clase ClientNetworkProtocolProperty)
  Establece el valor de cadena de la propiedad actual al que hace referencia el [Propertyidx (clase ClientNetworkProtocolProperty)](clientnetworkprotocolproperty-class.md) valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetStrValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ClientNetworkProtocolProperty](clientnetworkprotocolproperty-class.md) que representa un atributo del protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*strValue*|Valor de cadena que especifica el nuevo valor de la propiedad actual.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor unit 32 que es igual a 0 si se modificó el servicio correctamente, igual a 1 si no se admite la solicitud e igual a cualquier otro número para indicar que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
