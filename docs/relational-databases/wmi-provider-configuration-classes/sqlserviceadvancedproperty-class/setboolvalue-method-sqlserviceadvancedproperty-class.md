---
title: Método SetBoolValue (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
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
ms.openlocfilehash: cc9a2599daef295a8e326f19efa6f151685a050c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731390"
---
# <a name="setboolvalue-method-sqlserviceadvancedproperty-class"></a>Método SetBoolValue (clase SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
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
|*BoolValue*|Valor booleano que especifica el valor de la propiedad avanzada.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor **uint32** que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
 El tipo de valor de la propiedad debe ser booleano para establecer la propiedad en un valor booleano.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
