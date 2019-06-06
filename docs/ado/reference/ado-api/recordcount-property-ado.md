---
title: Propiedad RecordCount (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2b492476eadfde4c0c2666096714a8cd0f634db1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712025"
---
# <a name="recordcount-property-ado"></a>Propiedad RecordCount (ADO)

Indica el número de registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.
  
## <a name="return-value"></a>Valor devuelto

Devuelve un **largo** valor que indica el número de registros en el **Recordset**.
  
## <a name="remarks"></a>Comentarios

Use la **RecordCount** propiedad para averiguar cuántos registros se encuentran en un **Recordset** objeto. La propiedad devuelve -1 cuando ADO no puede determinar el número de registros o si no se admite el tipo de proveedor o el cursor **RecordCount**. Leer el **RecordCount** propiedad en un cerrado **Recordset** produce un error.

#### <a name="bookmarks-or-approximate-positioning"></a>Marcadores o una ubicación aproximada

Si el objeto Recordset *does* admite ambos marcadores o realizar una aproximación de ubicación, esta propiedad devuelve el número exacto de registros en el conjunto de registros. Esta propiedad devuelve el número exacto, independientemente de si el conjunto de registros ha rellenado por completo.

En cambio, si el objeto de conjunto de registros *no* admite marcadores o una ubicación aproximada, el acceso a esta propiedad puede ser un consumo significativo de recursos. La purga se produce porque todos los registros se deben recuperar y contar para devolver un valor de RecordCount preciso.

- **adBookmark** relacionados con marcadores.
- **adApproxPosition** se relaciona con una ubicación aproximada.

> [!NOTE]
> En las versiones 2.8 y versiones anteriores de ADO, el proveedor SQLOLEDB captura todos los registros cuando se utiliza un cursor de servidor, a pesar del hecho de que devuelve **True** para ambos **admite (adApproxPosition)** y **Admite (adBookmark)** .
  
El tipo de cursor de la **Recordset** afecta al objeto si se puede determinar el número de registros. El **RecordCount** propiedad devolverá -1 para un cursor de solo avance; el recuento real estático o de cursores; y -1 o el recuento real para un cursor dinámico, según el origen de datos.
  
## <a name="applies-to"></a>Se aplica a

[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también

[Ejemplo Filter y RecordCount propiedades (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Ejemplo Filter y RecordCount propiedades (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
