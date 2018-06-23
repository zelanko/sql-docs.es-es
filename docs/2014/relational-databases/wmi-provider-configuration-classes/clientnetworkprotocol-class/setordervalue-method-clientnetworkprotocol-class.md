---
title: Método SetOrderValue (clase ClientNetworkProtocol) | Documentos de Microsoft
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
- SetOrderValue Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ff50a3388fd83c23d13bc201c9c27ffc7f43fd44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113542"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>Método SetOrderValue (clase ClientNetworkProtocol)
  Selecciona el protocolo con el valor de orden especificado en la lista de protocolos del cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetOrderValue(  
OrderValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase ClientNetworkProtocol](clientnetworkprotocol-class.md) que representa el protocolo de red utilizado por el cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*OrderValue*|Valor u`int32` que establece el valor de orden.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de los protocolos de cliente (pestaña Ordenar)](http://technet.microsoft.com/library/ms187884.aspx)  
  
  