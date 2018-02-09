---
title: Propiedad PageCount (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0ce12f42693b58a57ecc4a08c186027a054bc80
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="pagecount-property-ado"></a>PageCount (propiedad, ADO)
Indica cuántas páginas de datos la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) contiene el objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que indica el número de páginas en el **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **PageCount** propiedad para determinar cuántas páginas de datos están en el **Recordset** objeto. *Páginas* son grupos de registros cuyo tamaño es igual a la [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) configuración de la propiedad. Incluso aunque la última página esté incompleta porque hay menos registros que el **PageSize** valor, cuenta como una página adicional en el **PageCount** valor. Si el **Recordset** objeto no admite esta propiedad, el valor será -1 para indicar que la **PageCount** no es posible determinar.  
  
 Consulte la **PageSize** y [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedades para más acerca de la funcionalidad de página.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount y ejemplo de las propiedades PageSize (VC ++)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propiedad PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
