---
title: "Método CreateParameter (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c293e3a6e337e3c0331884bf1ee1eed57ad36003
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Crea un nuevo [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto con las propiedades especificadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **parámetro** objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Opcional. A **cadena** valor que contiene el nombre de la **parámetro** objeto.  
  
 *Tipo*  
 Opcional. A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor que especifica el tipo de datos de la **parámetro** objeto.  
  
 *Dirección*  
 Opcional. A [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valor que especifica el tipo de **parámetro** objeto.  
  
 *Tamaño*  
 Opcional. A **largo** valor que especifica la longitud máxima para el valor del parámetro en caracteres o bytes.  
  
 *Valor*  
 Opcional. A **Variant** que especifica el valor de la **parámetro** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CreateParameter** método para crear un nuevo **parámetro** objeto con un nombre especificado, el tipo, la dirección, el tamaño y el valor. Cualquier valor que pase los argumentos de entrada se escribe en la correspondiente **parámetro** propiedades.  
  
 Este método no anexa automáticamente el **parámetro** el objeto a la **parámetros** colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Esto le permite establecer propiedades adicionales cuyos valores ADO validará cuando anexe el **parámetro** objeto a la colección.  
  
 Si se especifica un tipo de datos de longitud variable en el *tipo* argumento, debe pasar un *tamaño* argumento o un conjunto el [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md) propiedad de la **parámetro**  objeto antes de anexarlo a la **parámetros** colección; en caso contrario, se produce un error.  
  
 Si especifica un tipo de datos numéricos (**adNumeric** o **adDecimal**) en el *tipo* argumento; a continuación, debe establecer también la [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) y [Precisión](../../../ado/reference/ado-api/precision-property-ado.md) propiedades.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar y ejemplo de los métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar y ejemplo de los métodos CreateParameter (VC ++)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Objeto de parámetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
