---
title: Propiedad Properties (clase ServerNetworkProtocol) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 71e99af016ab114eecaa170374f9e07bf53bd3f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933669"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Propiedad Properties (clase ServerNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene las propiedades asociadas al protocolo de red del servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ServerNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) que representa el protocolo de red utilizado por la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Matriz de objetos de la [clase ServerNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) que representa las propiedades admitidos por el protocolo de red del servidor.  
  
## <a name="remarks"></a>Comentarios  
  
