---
title: Método AppendChunk (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 092419c105249df56e4258ccc3555e504c2e6b57
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="appendchunk-method-ado"></a>Método AppendChunk (ADO)
Anexa datos a un texto de gran tamaño o datos binarios [campo](../../../ado/reference/ado-api/field-object.md), o a un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parámetros  
 *objeto*  
 A **campo** o **parámetro** objeto.  
  
 *Datos*  
 A **Variant** que contiene los datos que se va a anexar al objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **AppendChunk** método en un **campo** o **parámetro** objeto que se va a rellenar con datos binarios largos o de caracteres. En situaciones donde la memoria del sistema es limitada, puede usar el **AppendChunk** método para manipular los valores largos en partes en lugar de en su totalidad.  
  
## <a name="field"></a>Campo  
 Si el **adFldLong** de bits en el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad de un **campo** objeto se establece en **true**, puede usar el  **AppendChunk** método para ese campo.  
  
 La primera **AppendChunk** llamar en un **campo** objeto escribe datos en el campo, sobrescribiendo los datos existentes. Posteriores **AppendChunk** agregan llamadas a los datos existentes. Si va a anexar datos a un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO supone que haya terminado de anexar datos al primer campo. Si se llama a la **AppendChunk** método en el primer campo una vez más, ADO interpreta la llamada como una nueva **AppendChunk** operación y sobrescribe los datos existentes. Obtener acceso a campos de otros [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que no son clones del primer **Recordset** no interrumpirá el objeto **AppendChunk** operaciones.  
  
 Si no hay ningún registro actual cuando se llama a **AppendChunk** en un **campo** del objeto, se produce un error.  
  
> [!NOTE]
>  El **AppendChunk** método no funciona en **campo** objetos de un [registro ADO (objetos)](../../../ado/reference/ado-api/record-object-ado.md) objeto. No realiza ninguna operación y se producirá un error de tiempo de ejecución.  
  
## <a name="parameter"></a>Parámetro  
 Si el **adParamLong** de bits en el **atributos** propiedad de un **parámetro** objeto se establece en **true**, puede usar el  **AppendChunk** método para ese parámetro.  
  
 La primera **AppendChunk** llamar en un **parámetro** objeto escribe datos en el parámetro, sobrescribiendo los datos existentes. Posteriores **AppendChunk** llama en un **parámetro** agregar objetos a los datos de parámetro existentes. Un **AppendChunk** llamada que pasa un valor null descarta todos los datos de parámetro.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo AppendChunk y GetChunk métodos (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Ejemplo AppendChunk y GetChunk métodos (VC ++)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
