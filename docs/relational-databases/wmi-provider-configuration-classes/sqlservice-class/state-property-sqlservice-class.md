---
title: Estado, propiedad (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
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
manager: craigg
ms.openlocfilehash: bed08f87e3d93eb3d18a86fd0931a4359a67ffea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644173"
---
# <a name="state-property-sqlservice-class"></a>Propiedad State (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
