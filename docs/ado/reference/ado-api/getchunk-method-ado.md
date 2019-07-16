---
title: Método GetChunk (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43c5fef08d22364b9842c58fc82d46ba4bfa00bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918565"
---
# <a name="getchunk-method-ado"></a>Método GetChunk (ADO)
Devuelve todo o parte del contenido de un texto grande o datos binarios [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Variant**.  
  
#### <a name="parameters"></a>Parámetros  
 *Tamaño*  
 Un **largo** expresión que es igual al número de bytes o caracteres que se van a recuperar.  
  
## <a name="remarks"></a>Comentarios  
 Use la **GetChunk** método en un **campo** objeto para recuperar la totalidad o parte de sus datos de caracteres o binarios largos. En situaciones donde se limita la memoria del sistema, puede usar el **GetChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
 Los datos que un **GetChunk** devoluciones de llamada se asigna a *variable*. Si *tamaño* es mayor que los datos restantes, el **GetChunk** método devuelve sólo los datos restantes sin relleno *variable* con espacios en blanco. Si el campo está vacío, el **GetChunk** método devuelve un valor null.  
  
 Cada uno de ellos posteriores **GetChunk** llamada recupera datos a partir de dónde anterior **GetChunk** llamada lo dejó. Sin embargo, si va a recuperar datos de un campo y, a continuación, puede establecer o leer el valor de otro campo en el registro actual, ADO supone que ha terminado de recuperar datos desde el primer campo. Si se llama a la **GetChunk** método en el primer campo de nuevo, ADO interpreta la llamada como un nuevo **GetChunk** operación y se inicia desde el principio de los datos de lectura. Obtener acceso a campos de otros [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que no son clones del primer **Recordset** objeto, no se interrumpirán **GetChunk** operaciones.  
  
 Si el **adFldLong** bit en el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad de un **campo** objeto se establece en **True**, puede usar el **GetChunk**  método para ese campo.  
  
 Si no hay ningún registro actual cuando se usa el **GetChunk** método en un **campo** objeto, se produce el error 3021 (no hay registro actual).  
  
> [!NOTE]
>  El **GetChunk** método no funciona en **campo** objetos de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. No realiza ninguna operación y se producirá un error de tiempo de ejecución.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [AppendChunk y GetChunk métodos ejemplo (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Ejemplo AppendChunk y GetChunk métodos (VC ++)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
