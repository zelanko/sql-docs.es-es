---
title: Método AppendChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ac0174a223571e29973ad854f9350a6e60f1de9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812003"
---
# <a name="appendchunk-method-ado"></a>Método AppendChunk (ADO)
Anexa datos a un texto grande o datos binarios [campo](../../../ado/reference/ado-api/field-object.md), o a un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parámetros  
 *object*  
 Un **campo** o **parámetro** objeto.  
  
 *Datos*  
 Un **Variant** que contiene los datos que se va a anexar al objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **AppendChunk** método en un **campo** o **parámetro** objeto para llenarlo con datos binarios largos o de caracteres. En situaciones donde se limita la memoria del sistema, puede usar el **AppendChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
## <a name="field"></a>Campo  
 Si el **adFldLong** bit en el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad de un **campo** objeto se establece en **true**, puede usar el  **AppendChunk** método para ese campo.  
  
 La primera **AppendChunk** llamar en un **campo** objeto escribe datos en el campo, sobrescribiendo los datos existentes. Posteriores **AppendChunk** agregan llamadas a los datos existentes. Si va a anexar datos a un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO se da por supuesto que haya terminado de anexar datos al primer campo. Si se llama a la **AppendChunk** método en el primer campo de nuevo, ADO interpreta la llamada como un nuevo **AppendChunk** operación y sobrescribe los datos existentes. Obtener acceso a campos de otros [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que no son clones del primer **Recordset** objeto, no se interrumpirán **AppendChunk** operaciones.  
  
 Si no hay ningún registro actual cuando se llama a **AppendChunk** en un **campo** objeto, se produce un error.  
  
> [!NOTE]
>  El **AppendChunk** método no funciona en **campo** objetos de un [registro ADO (objetos)](../../../ado/reference/ado-api/record-object-ado.md) objeto. No realiza ninguna operación y se producirá un error de tiempo de ejecución.  
  
## <a name="parameter"></a>Parámetro  
 Si el **adParamLong** bit en el **atributos** propiedad de un **parámetro** objeto se establece en **true**, puede usar el  **AppendChunk** método para ese parámetro.  
  
 La primera **AppendChunk** llamar en un **parámetro** objeto escribe datos en el parámetro, sobrescribiendo los datos existentes. Posteriores **AppendChunk** llama en un **parámetro** agregar objetos a los datos existentes de parámetro. Un **AppendChunk** llamada que se pasa un valor null descarta todos los datos de parámetro.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Field](../../../ado/reference/ado-api/field-object.md)|[Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vea también  
 [AppendChunk y GetChunk métodos ejemplo (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Ejemplo AppendChunk y GetChunk métodos (VC ++)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Método GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
