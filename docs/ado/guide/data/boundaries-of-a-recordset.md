---
title: Los límites de un conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 967ccb49cd2bbaa805420e7c982cc11721931022
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702350"
---
# <a name="boundaries-of-a-recordset"></a>Límites de un conjunto de registros
**Conjunto de registros** admite el **BOF** y **EOF** propiedades para delinear el principio y al final, respectivamente, del conjunto de datos. Puede pensar en **BOF** y **EOF** como registros "fantasmas" situados al principio y al final de la **Recordset**. Recuento **BOF** y **EOF**, nuestro ejemplo **Recordset** ahora tendría el aspecto siguiente:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Peras secos orgánicos de Bob tío|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|Manzanas secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 Cuando un cursor se mueve más allá del último registro, **EOF** está establecido en **True**; en caso contrario, su valor es **False**. De forma similar, cuando mueve el cursor delante del primer registro, **BOF** está establecido en **True**; en caso contrario, su valor es **False**. Estas propiedades se usan habitualmente para enumerar los registros del conjunto de datos, como se muestra en el siguiente fragmento de código JScript.  
  
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
  
 Si ambos **BOF** y **EOF** son **True**, **Recordset** objeto está vacío. Ambas propiedades será **False** para un recién abierto vacío **Recordset** objeto. Puede usar el **BOF** y **EOF** propiedades conjuntamente para determinar si un **Recordset** objeto está vacío o no, como se muestra en el siguiente fragmento de código JScript.  
  
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
  
 Este esquema funciona para todos los tipos de cursor y es independiente de los proveedores subyacentes. Si se intenta determinar el está vacía de un **Recordset** objeto comprobando si su **RecordCount** valor de propiedad es cero (0) o no, que debe tomar precauciones para utilizar un cursor apropiado y un proveedor que admite la devolución del número de registros en el resultado.  
  
 Si elimina el último registro que queda en el **Recordset** objeto, el cursor se deja en un estado indeterminado. El **BOF** y **EOF** propiedades pueden permanecer **False** hasta que se intente colocar el registro actual, dependiendo del proveedor. Para obtener más información, consulte [registros de eliminación mediante el método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
