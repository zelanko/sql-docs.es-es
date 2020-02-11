---
title: Método SetNumValue (clase SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumValue Method (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumValue method
ms.assetid: a5e1056b-0b75-4ad6-99c1-89246010d815
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f44d3426d7a3f11157167763e047dcb7423a904f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62635084"
---
# <a name="setnumvalue-method-sqlserviceadvancedproperty-class"></a>Método SetNumValue (clase SqlServiceAdvancedProperty)
  Establece el valor numérico de una propiedad.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object  
.SetNumValue(  
NumValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Objeto de la [clase SqlServiceAdvancedProperty](sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*NumValue*|Valor `uint32` que especifica el valor de la propiedad avanzada.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Observaciones  
 El tipo de valor de propiedad debe ser numérico para poder establecer la propiedad en un valor numérico.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar y detener servicios](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
