---
title: Filtrado para actualiza registros | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 529845297ff3c4264cc152c652b31c0bd12f5441
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270884"
---
# <a name="filtering-for-updated-records"></a>Filtrar registros actualizados
Antes de llamar a UpdateBatch, puede usar la propiedad de filtro de conjunto de registros para ver solo aquellos registros que se han cambiado desde que se abrió el conjunto de registros o la última llamada a UpdateBatch. Para ello, establezca Filter en adFilterPendingRecords para determinar cuántos registros se actualizarán, como se muestra en el ejemplo de código en la sección siguiente.  
  
## <a name="remarks"></a>Notas  
 En este ejemplo se amplía el ejemplo de UpdateBatch anterior filtrar el conjunto de registros antes de llamar a la UpdateBatch, que muestra al usuario que los registros cambiará y permitir que ella cancelar la actualización (mediante el método CancelBatch).  
  
```  
'BeginFilterPend  
    '...  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)
