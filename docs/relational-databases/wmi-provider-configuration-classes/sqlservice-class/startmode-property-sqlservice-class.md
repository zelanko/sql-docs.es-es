---
title: Propiedad StartMode (clase SqlService) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
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
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93802c3cc0e53b0996bd7db5d5a6bca959c4302a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="startmode-property-sqlservice-class"></a>Propiedad StartMode (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene el modo de inicio del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica el modo del servicio.  
  
 Los valores pueden ser alguno de los siguientes:  
  
 Arranque  
 Valor = 0. Servicio iniciado por el cargador del sistema operativo. Esta opción solo es válida para los servicios del controlador.  
  
 Sistema  
 Valor = 1. Servicio iniciado por el **IoInitSystem** método. Esta opción solo es válida para los servicios del controlador.  
  
 Automático  
 Valor = 2. Servicio que el administrador de control de servicios iniciará automáticamente durante el inicio del sistema.  
  
 Manual  
 Valor = 3. Servicio se inicie el Administrador de equipo cuando un proceso llame el **StartService** método.  
  
 Deshabilitado  
 Valor = 4. El servicio no se puede iniciar.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
