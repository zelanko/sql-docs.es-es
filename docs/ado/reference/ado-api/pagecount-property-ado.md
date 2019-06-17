---
title: PageCount (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5187c73d4dde95a5ddd9396da95b2d4381c868c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706940"
---
# <a name="pagecount-property-ado"></a>PageCount (propiedad, ADO)
Indica cuántas páginas de datos la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) contiene el objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que indica el número de páginas en el **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **PageCount** propiedad para determinar cuántas páginas de datos están en el **Recordset** objeto. *Páginas* son grupos de registros cuyo tamaño es igual a la [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) configuración de la propiedad. Incluso si la última página está incompleta porque hay menos registros que el **PageSize** valor, cuenta como una página adicional en el **PageCount** valor. Si el **Recordset** objeto no admite esta propiedad, el valor será -1 para indicar que el **PageCount** no es posible determinar.  
  
 Consulte la **PageSize** y [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedades para obtener más acerca de la funcionalidad de página.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VC ++)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propiedad PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
