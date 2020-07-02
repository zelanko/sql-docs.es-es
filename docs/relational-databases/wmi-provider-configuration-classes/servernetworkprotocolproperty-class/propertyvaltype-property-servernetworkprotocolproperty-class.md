---
title: Propiedad PropertyValType (ServerNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyValType Property (ServerNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 850bf40605701da98a5ecf5ce5a95cf276aa6e39
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727050"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>Propiedad PropertyValType (clase ServerNetworkProtocolProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene el tipo de datos del valor almacenado en la propiedad a la que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.PropertyValType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ServerNetworkProtocolProperty](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) que representa un atributo del Protocolo de red en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **UInt32** que especifica el tipo de datos del valor de propiedad. Devuelve 0 para un valor de cadena y 1 para un tipo numérico.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos y bibliotecas de red de servidores de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
