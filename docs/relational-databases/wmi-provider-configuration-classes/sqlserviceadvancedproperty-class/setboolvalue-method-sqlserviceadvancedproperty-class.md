---
title: Método SetBoolValue (clase SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetBoolValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetBoolValue method
ms.assetid: 5252b439-fce5-446a-8e57-99e3054bee69
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 99a456da7b3f452c94ab01bd3fc08215152ee2f5
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216833"
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>Método SetBoolValue (clase SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Establece el valor booleano de una propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.SetBoolValue [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Objeto de la [clase SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*ValorBOOL*|Valor booleano que especifica el valor de la propiedad avanzada.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
 El tipo de valor de la propiedad debe ser booleano para establecer la propiedad en un valor booleano.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
