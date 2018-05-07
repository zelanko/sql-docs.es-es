---
title: Método SetValue (clase ClientSettingsGeneralFlag) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SetValue Method (ClientSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: 34443689-a0e0-4668-a811-17532c6fd271
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 726e32390d58a9b1c3e1f80e2fca5b958b41fae5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setvalue-method-clientsettingsgeneralflag-class"></a>Método SetValue (clase ClientSettingsGeneralFlag)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Establece todos los valores de la marca a la que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase ClientSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md) que representa una marca general para la configuración del servidor.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*Valor*|Valor booleano que especifica el valor de la marca.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Configurar protocolos de cliente](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
