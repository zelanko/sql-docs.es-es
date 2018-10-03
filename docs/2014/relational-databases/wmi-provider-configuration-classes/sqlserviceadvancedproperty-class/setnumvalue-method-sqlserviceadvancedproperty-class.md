---
title: Método SetNumValue (clase SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
ms.openlocfilehash: 7f31ef35b465467a00b6fe791c57d6d30f3e5069
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161015"
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
 *object*  
 Objeto de la [clase SqlServiceAdvancedProperty](sqlserviceadvancedproperty-class.md) que representa una propiedad avanzada.  
  
#### <a name="parameters"></a>Parámetros  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*NumValue*|Valor `uint32` que especifica el valor de la propiedad avanzada.|  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Valor `uint32` que es 0 si se modificó el servicio correctamente, 1 si no se admite la solicitud y cualquier otro número para indicar un error.  
  
## <a name="remarks"></a>Comentarios  
 El tipo de valor de propiedad debe ser numérico para poder establecer la propiedad en un valor numérico.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener servicios](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
