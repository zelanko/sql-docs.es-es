---
title: "Los límites de un conjunto de registros | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 66dec387cc91a2d0bd4d3aded73a6b4301aff593
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="boundaries-of-a-recordset"></a>Límites de un conjunto de registros
**Conjunto de registros** es compatible con la **BOF** y **EOF** propiedades para delinear el principio y al final, respectivamente, del conjunto de datos. Puede pensar en **BOF** y **EOF** como "registros"fantasma situados al principio y al final de"la **conjunto de registros**. Recuento de **BOF** y **EOF**, nuestro ejemplo **Recordset** ahora sería similar al siguiente:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Peras secas orgánicas de tío Bob|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle chucrut|45.6000|  
|51|Manzanas secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 Cuando un cursor se mueve más allá del último registro, **EOF** está establecido en **True**; en caso contrario, su valor es **False**. De forma similar, cuando se mueve el cursor delante del primer registro, **BOF** está establecido en **True**; en caso contrario, su valor es **False**. Estas propiedades se utilizan habitualmente para enumerar los registros del conjunto de datos, como se muestra en el siguiente fragmento de código JScript.  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 Si ambos **BOF** y **EOF** son **True**, **Recordset** objeto está vacío. Ambas propiedades será **False** para un recién abierta, no está vacío **Recordset** objeto. Puede usar el **BOF** y **EOF** propiedades conjuntamente para determinar si un **Recordset** objeto está vacío o no, como se muestra en el siguiente fragmento de código JScript.  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 Este esquema funciona con todos los tipos de cursor y es independiente de los proveedores subyacentes. Si intenta determinar la está vacía de un **Recordset** objeto comprobando si su **RecordCount** valor de la propiedad es cero (0) o no, debe tomar precauciones para usar un cursor adecuado y un proveedor que compatible con la devolución del número de registros en el resultado.  
  
 Si elimina el último registro que queda en el **Recordset** de objeto, el cursor se deja en un estado indeterminado. El **BOF** y **EOF** propiedades pueden permanecer **False** hasta que se intente volver a colocar el registro actual, dependiendo del proveedor. Para obtener más información, consulte [registros de eliminación mediante el método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).

