---
title: Método CreateParameter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 251c35977421d63027fbc9d6042e193125da854d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695636"
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
 *Name*  
 Opcional. Un **cadena** valor que contiene el nombre de la **parámetro** objeto.  
  
 *Tipo*  
 Opcional. Un [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valor que especifica el tipo de datos de la **parámetro** objeto.  
  
 *Dirección*  
 Opcional. Un [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valor que especifica el tipo de **parámetro** objeto.  
  
 *Tamaño*  
 Opcional. Un **largo** valor que especifica la longitud máxima para el valor del parámetro en caracteres o bytes.  
  
 *Valor*  
 Opcional. Un **Variant** que especifica el valor para el **parámetro** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CreateParameter** método para crear un nuevo **parámetro** objeto con un nombre especificado, el tipo, la dirección, el tamaño y el valor. Cualquier valor que pase los argumentos se escribe en la correspondiente **parámetro** propiedades.  
  
 Este método no anexa automáticamente el **parámetro** de objeto para el **parámetros** colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto. Esto le permite establecer propiedades adicionales cuyos valores ADO validará al anexar el **parámetro** objeto a la colección.  
  
 Si se especifica un tipo de datos de longitud variable en el *tipo* argumento, se debe pasar un *tamaño* argumento o un conjunto el [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md) propiedad de la **parámetro**  objeto antes de agregarlo a la **parámetros** colección; en caso contrario, se produce un error.  
  
 Si especifica un tipo de datos numéricos (**adNumeric** o **adDecimal**) en el *tipo* argumento, a continuación, se debe establecer también la [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) y [Precisión](../../../ado/reference/ado-api/precision-property-ado.md) propiedades.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Anexar y ejemplo de los métodos CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anexar y ejemplo de los métodos CreateParameter (VC ++)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Objeto de parámetro](../../../ado/reference/ado-api/parameter-object.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
