---
title: Método SetEnable (clase ServerNetworkProtocolIPAddress) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ServerNetworkProtocolIPAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: baa86deb-95dd-416f-b2c7-cec1dfb91ab4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5b29208532f39b814aa855b78aa953c7c6f77310
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216303"
---
# <a name="setenable-method-servernetworkprotocolipaddress-class"></a>Método SetEnable (clase ServerNetworkProtocolIPAddress)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Habilita la dirección IP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetEnable()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ServerNetworkProtocolIPAdress](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) que representa una dirección IP del protocolo de red en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y las bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
