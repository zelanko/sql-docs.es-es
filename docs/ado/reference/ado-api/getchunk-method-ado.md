---
title: GetChunk (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f41cd6a590c318f3268eb5292b2086685a36848
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760061"
---
# <a name="getchunk-method-ado"></a>Método GetChunk (ADO)
Devuelve todo, o una parte, del contenido de un objeto de [campo](../../../ado/reference/ado-api/field-object.md) de datos binarios o de texto grande.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **valor de tipo Variant**.  
  
#### <a name="parameters"></a>Parámetros  
 *Size*  
 Expresión **larga** que es igual al número de bytes o caracteres que se desea recuperar.  
  
## <a name="remarks"></a>Comentarios  
 Use el método **GetChunk** en un objeto de **campo** para recuperar parte o todos los datos binarios o de caracteres largos. En situaciones en las que la memoria del sistema es limitada, puede utilizar el método **GetChunk** para manipular valores largos en partes, en lugar de en su totalidad.  
  
 Los datos que devuelve una llamada a **GetChunk** se asignan a la *variable*. Si el *tamaño* es mayor que el resto de los datos, el método **GetChunk** devuelve solo los datos restantes sin la *variable* padding con espacios vacíos. Si el campo está vacío, el método **GetChunk** devuelve un valor null.  
  
 Cada llamada a **GetChunk** subsiguiente recupera datos a partir de donde se dejó la anterior llamada a **GetChunk** . Sin embargo, si va a recuperar datos de un campo y, a continuación, establece o lee el valor de otro campo en el registro actual, ADO supone que ha terminado de recuperar los datos del primer campo. Si llama de nuevo al método **GetChunk** en el primer campo, ADO interpreta la llamada como una nueva operación **GetChunk** y comienza a leer desde el principio de los datos. El acceso a los campos de otros objetos de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) que no sean clones del primer objeto de **conjunto de registros** no interrumpirá las operaciones de **GetChunk** .  
  
 Si el **bit adFldLong** en la propiedad [attributes](../../../ado/reference/ado-api/attributes-property-ado.md) de un objeto **Field** está establecido en **true**, puede utilizar el método **GetChunk** para ese campo.  
  
 Si no hay ningún registro actual cuando se usa el método **GetChunk** en un objeto de **campo** , se produce el error 3021 (no hay registro actual).  
  
> [!NOTE]
>  El método **GetChunk** no funciona en objetos de **campo** de un objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) . No realiza ninguna operación y producirá un error en tiempo de ejecución.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos AppendChunk y GetChunk (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Ejemplo de los métodos AppendChunk y GetChunk (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk (método) (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
