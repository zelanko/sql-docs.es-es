---
title: Propiedad AcceptStop (clase SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 26889228181b16c7ea58560708766d048b939f0d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656694"
---
# <a name="acceptstop-property-sqlservice-class"></a>Propiedad AcceptStop (clase SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtiene el valor de propiedad booleano que especifica si se puede detener el servicio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Un [clase SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) objeto que representa el servicio  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Un valor booleano que especifica si se puede detener el servicio: **true** si se puede detener el servicio, o **false** si no se puede detener el servicio.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
