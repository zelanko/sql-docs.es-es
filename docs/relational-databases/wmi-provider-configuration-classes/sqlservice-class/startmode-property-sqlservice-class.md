---
title: Propiedad StartMode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartMode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1adda63135bc85ae2d8a84a8e8744b04144781de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85662115"
---
# <a name="startmode-property-sqlservice-class"></a>Propiedad StartMode (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene el modo de inicio del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.StartMode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica el modo del servicio.  
  
 Los valores pueden ser alguno de los siguientes:  
  
 Arranque  
 Valor = 0. Servicio iniciado por el cargador del sistema operativo. Esta opción solo es válida para los servicios del controlador.  
  
 Sistema  
 Valor = 1. Servicio Iniciado por el método **IoInitSystem** . Esta opción solo es válida para los servicios del controlador.  
  
 Automático  
 Valor = 2. Servicio que el administrador de control de servicios iniciará automáticamente durante el inicio del sistema.  
  
 Manual  
 Valor = 3. Servicio que el administrador de equipo iniciará cuando un proceso llame al método **StartService** .  
  
 Disabled  
 Valor = 4. El servicio no se puede iniciar.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
