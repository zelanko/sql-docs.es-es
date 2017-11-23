---
title: "Método SetBoolValue (clase SqlServiceAdvancedProperty) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetBoolValue Method (SqlServiceAdvancedProperty Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetBoolValue method
ms.assetid: 5252b439-fce5-446a-8e57-99e3054bee69
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59d85173e1a95e767f8357ccb944673c015d0e1f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>Método SetBoolValue (clase SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Establece el valor booleano de una propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetBoolValue [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*ValorBOOL*|Valor booleano que especifica el valor de la propiedad avanzada.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
 El tipo de valor de la propiedad debe ser booleano para establecer la propiedad en un valor booleano.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
