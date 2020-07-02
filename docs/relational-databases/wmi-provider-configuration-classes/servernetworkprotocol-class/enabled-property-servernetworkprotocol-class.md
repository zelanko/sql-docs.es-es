---
title: Propiedad Enabled (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: a514822a-91f1-4aca-9175-2b96cff29700
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 32ad06a57dccfa2f36e7990d38d5bafa7310144f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750072"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Propiedad Enabled (clase ServerNetworkProtocol)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene la propiedad booleana que especifica si el protocolo de red del servidor está habilitado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ServerNetworkProtocol](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md) que representa el protocolo de red utilizado por la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor booleano que especifica si el protocolo de red del servidor está habilitado: **true** si el protocolo de red del servidor está habilitado; en caso contrario, **false** .  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos y bibliotecas de red de servidores de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
