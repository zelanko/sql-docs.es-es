---
title: Método GetChunk (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d39075e6d3c16540ded137a8ac78ccc6f8d94f8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278794"
---
# <a name="getchunk-method-ado"></a>Método GetChunk (ADO)
Devuelve todo o una parte del contenido de un texto de gran tamaño o datos binarios [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Variant**.  
  
#### <a name="parameters"></a>Parámetros  
 *Tamaño*  
 A **largo** expresión que es igual al número de bytes o caracteres que se van a recuperar.  
  
## <a name="remarks"></a>Notas  
 Use la **GetChunk** método en un **campo** objeto que se va a recuperar la parte o la totalidad de sus datos binarios largos o de caracteres. En situaciones donde la memoria del sistema es limitada, puede usar el **GetChunk** método para manipular los valores largos en partes, en lugar de en su totalidad.  
  
 Los datos que un **GetChunk** devoluciones de llamada se asigna a *variable*. Si *tamaño* es mayor que el resto de los datos, el **GetChunk** método devuelve sólo los datos restantes sin relleno *variable* con espacios en blanco. Si el campo está vacío, el **GetChunk** método devuelve un valor null.  
  
 Cada uno de ellos posteriores **GetChunk** llamada recupera datos a partir de donde anterior **GetChunk** dejó de llamada. Sin embargo, si va a recuperar datos de un campo y, a continuación, establecer o leer el valor de otro campo en el registro actual, ADO supone que ha terminado de recuperar datos desde el primer campo. Si se llama a la **GetChunk** método en el primer campo una vez más, ADO interpreta la llamada como una nueva **GetChunk** operación e inicia leer desde el principio de los datos. Obtener acceso a campos de otros [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que no son clones del primer **Recordset** no interrumpirá el objeto **GetChunk** operaciones.  
  
 Si el **adFldLong** de bits en el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propiedad de un **campo** objeto se establece en **True**, puede usar el **GetChunk**  método para ese campo.  
  
 Si no hay ningún registro actual cuando se usa el **GetChunk** método en un **campo** del objeto, se produce el error 3021 (no hay registro actual).  
  
> [!NOTE]
>  El **GetChunk** método no funciona en **campo** objetos de un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto. No realiza ninguna operación y se producirá un error de tiempo de ejecución.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo AppendChunk y GetChunk métodos (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Ejemplo AppendChunk y GetChunk métodos (VC ++)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Método AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
