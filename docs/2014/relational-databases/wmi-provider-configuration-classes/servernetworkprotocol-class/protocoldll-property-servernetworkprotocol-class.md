---
title: Propiedad ProtocolDLL (clase ServerNetworkProtocol) | Documentos de Microsoft
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
- ProtocolDLL Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolDLL property
ms.assetid: ac386558-392e-46f3-97f8-382f267b7fca
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3b0daf8b5d2db8ccce3622db5cbfe92643f62261
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196876"
---
# <a name="protocoldll-property-servernetworkprotocol-class"></a>Propiedad ProtocolDLL (clase ServerNetworkProtocol)
  Obtiene el nombre del archivo .dll requerido por un protocolo de red del servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [clase ServerNetworkProtocol](servernetworkprotocol-class.md) objeto que representa el protocolo de red utilizado por la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor de cadena que especifica el archivo .dll de protocolo requerido por el protocolo de red del servidor.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de red de servidor y bibliotecas de red](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  