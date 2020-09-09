---
description: Propiedad MultiIpConfigurationSupport (clase ServerNetworkProtocol)
title: Propiedad MultiIpConfigurationSupport (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9a0c29f72ab66f008dfe6ddfb87be054501aeb50
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545492"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>Propiedad MultiIpConfigurationSupport (clase ServerNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene la propiedad booleana que especifica si un protocolo de red del servidor admite varias direcciones IP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [propiedad ProtocolName (clase ServerNetworkProtocol)](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md) que representa el protocolo de red utilizado por la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor booleano que especifica si el protocolo de red del servidor admite varias direcciones IP: **true** si el protocolo de red del servidor admite varias direcciones IP, o **false** si el protocolo de red del servidor no admite varias direcciones IP.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos y bibliotecas de red de servidores de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
