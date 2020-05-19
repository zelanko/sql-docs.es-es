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
author: rothja
ms.author: jroth
ms.openlocfilehash: c936eb8016be0851fa6d3ecff1f624eab6c895f3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748676"
---
# <a name="clone-method-ado"></a>Clone (método) (ADO)
Crea un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) duplicado a partir de un objeto de conjunto de **registros** existente. Opcionalmente, especifica que el clon es de solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve una referencia de objeto de **conjunto de registros** .  
  
#### <a name="parameters"></a>Parámetros  
 *rstDuplicate*  
 Variable de objeto que identifica el objeto de **conjunto de registros** duplicado que se va a crear.  
  
 *rstOriginal*  
 Variable de objeto que identifica el objeto de **conjunto de registros** que se va a duplicar.  
  
 *LockType*  
 Opcional. Valor de [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que especifica el tipo de bloqueo del conjunto de **registros**original o un **conjunto de registros**de solo lectura. Los valores válidos son **adLockUnspecified** o **adLockReadOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Utilice el método **Clone** para crear varios objetos **Recordset** duplicados, especialmente si desea mantener más de un registro actual en un conjunto determinado de registros. Usar el método **Clone** es más eficaz que crear y abrir un nuevo objeto de **conjunto de registros** que use la misma definición que el original.  
  
 La propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) del conjunto de **registros**original, si existe, no se aplicará al clon. Establezca la propiedad **Filter** del nuevo **conjunto de registros** para filtrar los resultados. La manera más sencilla de copiar cualquier valor de **filtro** existente es asignarlo directamente, como se indica a continuación.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 El registro actual de un clon recién creado se establece en el primer registro.  
  
 Los cambios que realice en un objeto de **conjunto de registros** serán visibles en todos sus clones, independientemente del tipo de cursor. Sin embargo, después de ejecutar [Requery](../../../ado/reference/ado-api/requery-method.md) en el **conjunto de registros**original, los clones ya no se sincronizarán con el original.  
  
 Al cerrar el **conjunto de registros** original no se cierran sus copias, ni al cerrar una copia se cierra el original o cualquiera de las demás copias.  
  
 Solo puede clonar un objeto de **conjunto de registros** que admita marcadores. Los valores de marcador son intercambiables. es decir, una referencia de marcador de un objeto de **conjunto de registros** hace referencia al mismo registro en cualquiera de sus clones.  
  
 Algunos eventos de **conjunto de registros** que se desencadenan también se producirán en todos los clones del **conjunto de registros** . Sin embargo, dado que el registro actual puede diferir entre los **conjuntos de registros**clonados, es posible que los eventos no sean válidos para el clon. Por ejemplo, si cambia un valor de un campo, se producirá un evento [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) en el **conjunto de registros** cambiado y en todos los clones. El parámetro *Fields* del evento **WillChangeField** de un conjunto de **registros** clonado (donde no se realizó el cambio) hará referencia a los campos del registro actual del clon, que puede ser un registro diferente del registro actual del **conjunto de registros** original en el que se produjo el cambio.  
  
 En la tabla siguiente se proporciona una lista completa de todos los eventos de **conjunto de registros** . Indica si son válidos y se desencadenan para los clones de conjunto de registros generados mediante el método **Clone** .  
  
|Evento|¿Se desencadena en clones?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|No|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|No|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|No|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Yes|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Yes|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Yes|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Yes|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Clone (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Ejemplo del método Clone (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Ejemplo del método Clone (VC ++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
