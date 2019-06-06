---
title: Clone (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fbeedf9e56c1f0606a7c8f842baedc9d11ad3929
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698798"
---
# <a name="clone-method-ado"></a>Clone (método) (ADO)
Crea un duplicado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto a partir de una máquina **Recordset** objeto. Opcionalmente, especifica que la clonación sea de sólo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Recordset** referencia de objeto.  
  
#### <a name="parameters"></a>Parámetros  
 *rstDuplicate*  
 Una variable de objeto que identifica el duplicado **Recordset** objeto que se va a crearse.  
  
 *rstOriginal*  
 Una variable de objeto que identifica el **Recordset** objeto duplicado.  
  
 *LockType*  
 Opcional. Un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valor que especifica el tipo de bloqueo del original **Recordset**, o solo lectura **Recordset**. Los valores válidos son **adLockUnspecified** o **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **clon** duplicar el método para crear varios **Recordset** objetos, especialmente si desea mantener más de un registro actual en un determinado conjunto de registros. Mediante el **clon** es más eficaz que crear y abrir un nuevo método **Recordset** objeto que usa la misma definición que el original.  
  
 El [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad del original **Recordset**, si existe, no se aplicará al clon. Establecer el **filtro** propiedad del nuevo **Recordset** para filtrar los resultados. La manera más sencilla de copiar cualquier existente **filtro** valor es asignarlo directamente, como se indica a continuación.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 El registro actual de un clon recién creado se establece en el primer registro.  
  
 Cambios en uno **Recordset** objeto están visibles en todos sus clones, independientemente del tipo de cursor. Sin embargo, después de ejecutar [Requery](../../../ado/reference/ado-api/requery-method.md) en el original **Recordset**, los clones ya no se sincronizarán con el original.  
  
 Cierre el original **Recordset** no cierra sus copias, ni tampoco cerrar cierre una copia del original, o cualquiera de las demás copias.  
  
 Solo puede clonar un **Recordset** objeto que admite marcadores. Los valores de marcador son intercambiables; es decir, una referencia de marcador de un **Recordset** objeto hace referencia en el mismo registro en cualquiera de sus clones.  
  
 Algunos **Recordset** eventos desencadenados por también se producirán en todos los **Recordset** clones. Sin embargo, dado que el registro actual puede diferir entre clonar **conjuntos de registros**, los eventos no sean válidos para el clon. Por ejemplo, si cambia un valor de un campo, un [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) se producirá el evento en los cambios **Recordset** y en todos los duplicados. El *campos* parámetro de la **WillChangeField** eventos de clonado **Recordset** (donde no se ha realizado el cambio) hará referencia a los campos del registro actual del clon, lo que puede ser un registro diferente que el registro actual del original **Recordset** donde se produjo el cambio.  
  
 En la tabla siguiente proporciona una lista completa de todos los **Recordset** eventos. Indica si son válidos y desencadenadas para cualquier clones de conjunto de registros generados mediante la **clon** método.  
  
|Evento|¿Se desencadena en los duplicados?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|Sin|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|Sin|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|No|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sí|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Sin|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sí|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sí|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sí|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|Sin|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|Sin|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Clone (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Ejemplo del método Clone (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Ejemplo del método Clone (VC ++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
