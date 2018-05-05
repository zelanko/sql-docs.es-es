---
title: Propiedad RecordCount (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67416b2282f913e04867b9d4ac23ee0ea0f0c41a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="recordcount-property-ado"></a>Propiedad RecordCount (ADO)

Indica el número de registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.
  
## <a name="return-value"></a>Valor devuelto

Devuelve un **largo** valor que indica el número de registros en la **conjunto de registros**.
  
## <a name="remarks"></a>Comentarios

Use la **RecordCount** propiedad para averiguar cuántos registros se encuentran en un **Recordset** objeto. La propiedad devuelve -1 cuando ADO no puede determinar el número de registros o si el tipo de proveedor o el cursor no admite **RecordCount**. Leer la **RecordCount** propiedad en un cerrado **Recordset** produce un error.

#### <a name="bookmarks-or-approximate-positioning"></a>Marcadores o una ubicación aproximada

Si el objeto de conjunto de registros *does* admite ambos marcadores o aproximado posición, esta propiedad devuelve el número exacto de registros en el conjunto de registros. Esta propiedad devuelve el número exacto, independientemente de si el conjunto de registros se hayan llenado completamente.

En cambio, si el objeto de conjunto de registros *no* admite marcadores o una ubicación aproximada, obtener acceso a esta propiedad puede ser un consumo significativo de recursos. La purga se produce porque todos los registros se deben recuperar y contar para devolver un valor de RecordCount preciso.

- **adBookmark** relacionados con marcadores.
- **adApproxPosition** se relaciona con una ubicación aproximada.

> [!NOTE]
> En versiones de ADO 2,8 y versiones anteriores, el proveedor SQLOLEDB captura todos los registros cuando se utiliza un cursor de servidor, a pesar del hecho que devuelve **True** para ambos **admite (adApproxPosition)** y **Admite (adBookmark)**.
  
El tipo de cursor de la **Recordset** objeto determina si se puede determinar el número de registros. El **RecordCount** propiedad devolverá -1 para un cursor de sólo avance; el recuento real para una variable static o cursor de conjunto de claves y -1 o el recuento real para un cursor dinámico, según el origen de datos.
  
## <a name="applies-to"></a>Se aplica a

[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también

[Filtro y ejemplo de las propiedades RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filtro y ejemplo de las propiedades RecordCount (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
