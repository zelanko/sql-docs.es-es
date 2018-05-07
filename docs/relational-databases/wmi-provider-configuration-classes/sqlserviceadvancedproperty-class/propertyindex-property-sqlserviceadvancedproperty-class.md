---
title: Propiedad PropertyIndex (clase SqlServiceAdvancedProperty) | Documentos de Microsoft
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
- PropertyIndex Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIndex property
ms.assetid: b18b45a2-e187-44f5-a8c9-26fd9828b6c6
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 358d1040f833d1f6e286c7a08e6fa72d816bca11
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="propertyindex-property-sqlserviceadvancedproperty-class"></a>Propiedad PropertyIndex (clase SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene o establece el índice de propiedad que especifica la posición de una propiedad avanzada en una matriz de propiedades avanzadas que pertenecen a un servicio al que se hace referencia.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.PropertyIndex [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 A **uint32** valor que especifica la posición de la propiedad avanzada en la matriz de la propiedad avanzada que pertenece al servicio que se hace referencia.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
