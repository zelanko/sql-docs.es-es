---
title: Método SetDisable (clase ServerNetworkProtocolIPAddress) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ad30d27d63169d5b847e527febead00e3aaa516
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>Método SetDisable (clase ServerNetworkProtocolIPAddress)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Deshabilita la dirección IP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase ServerNetworkProtocolIPAdress](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) que representa una dirección IP del protocolo de red en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor unit 32 que es igual a 0 si se modificó el servicio correctamente, igual a 1 si no se admite la solicitud e igual a cualquier otro número para indicar que hubo un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
