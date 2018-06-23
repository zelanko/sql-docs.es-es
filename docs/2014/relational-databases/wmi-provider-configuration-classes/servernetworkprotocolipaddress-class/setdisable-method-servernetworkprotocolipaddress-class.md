---
title: Método SetDisable (clase ServerNetworkProtocolIPAddress) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetDisable Method (ServerNetworkProtocolIPAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDisable method
ms.assetid: 7a7cc8cc-9fb8-4bf5-b483-2150d633ee10
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 310660fed0cf74f7fef6367bfee4484a76446d72
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111108"
---
# <a name="setdisable-method-servernetworkprotocolipaddress-class"></a>Método SetDisable (clase ServerNetworkProtocolIPAddress)
  Deshabilita la dirección IP.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetDisable()  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un servernetworkprotocolipaddress [ServerNetworkProtocolIPAdress Class]-class.md) objeto que representa una dirección IP para el protocolo de red en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor unit 32 que es igual a 0 si se modificó el servicio correctamente, igual a 1 si no se admite la solicitud e igual a cualquier otro número para indicar que hubo un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  