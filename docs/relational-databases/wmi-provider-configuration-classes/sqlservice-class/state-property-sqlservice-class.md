---
title: Propiedad State (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- State Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f07d1a1db062060c00f29d0454ac4a4902b76fda
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85722719"
---
# <a name="state-property-sqlservice-class"></a>Propiedad State (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Obtiene o establece el estado actual del servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa el servicio.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor uint32 que especifica el estado del servicio.  
  
 Los valores pueden ser alguno de los siguientes:  
  
 1  
 Detenido. El servicio está detenido.  
  
 2  
 Inicio pendiente. El servicio está a la espera de que se inicie.  
  
 3  
 Detención pendiente. El servicio está a la espera de que se detenga.  
  
 4  
 En ejecución. El servicio se está ejecutando.  
  
 5  
 Continuación pendiente. El servicio está a la espera de continuar.  
  
 6  
 Pausa pendiente. El servicio está a la espera de que se ponga en pausa.  
  
 7  
 En pausa. El servicio está en pausa.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
