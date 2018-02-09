---
title: Propiedad RecordCount (ADO) | Documentos de Microsoft
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
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 92faeb5d2ec0b62c03292f71e0299c779e362478
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="recordcount-property-ado"></a>Propiedad RecordCount (ADO)
Indica el número de registros en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que indica el número de registros en la **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **RecordCount** propiedad para averiguar cuántos registros se encuentran en un **Recordset** objeto. La propiedad devuelve -1 cuando ADO no puede determinar el número de registros o si el tipo de proveedor o el cursor no admite **RecordCount**. Leer la **RecordCount** propiedad en un cerrado **Recordset** produce un error.  
  
 Si el **Recordset** objeto admite una ubicación aproximada o marcadores??? es decir, **admite (adApproxPosition)** o **admite (adBookmark)**, respectivamente, devolver **True**??? Este valor será el número exacto de registros en la **Recordset**, independientemente de si se ha rellenado por completo. Si el **Recordset** objeto no admite una ubicación aproximada, esta propiedad puede deberse a un consumo significativo de recursos tendrán todos los registros que se puedan recuperar y contar para devolver un tipo de objeto **RecordCount** valor.  
  
> [!NOTE]
>  En versiones de ADO 2,8 y versiones anteriores, el proveedor SQLOLEDB captura todos los registros cuando se utiliza un cursor de servidor, a pesar del hecho que devuelve **True** para ambos **admite (adApproxPosition)** y **Admite (adBookmark)**.  
  
 El tipo de cursor de la **Recordset** objeto determina si se puede determinar el número de registros. El **RecordCount** propiedad devolverá -1 para un cursor de sólo avance; el recuento real para una variable static o cursor de conjunto de claves y -1 o el recuento real para un cursor dinámico, según el origen de datos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Filtro y ejemplo de las propiedades RecordCount (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [Filtro y ejemplo de las propiedades RecordCount (VC ++)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Propiedad AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
