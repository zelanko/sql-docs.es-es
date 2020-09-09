---
description: Propiedad IpAddresses (clase ServerNetworkProtocol)
title: Propiedad IpAddresses (ServerNetworkProtocol)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- IpAddresses Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9bd31cf4758415cc235942607319a26c1a283437
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545469"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>Propiedad IpAddresses (clase ServerNetworkProtocol)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene las direcciones IP asociadas al protocolo de red del servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.IpAddresses [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un objeto **ServerNetworkProtocol** que representa el protocolo de red utilizado por la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Matriz de objetos de la [clase ServerNetworkProtocolIPAdress](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) que representan las direcciones IP admitidas por el protocolo de red del servidor.  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="see-also"></a>Consulte también  
 [Configurar protocolos y bibliotecas de red de servidores de red](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
