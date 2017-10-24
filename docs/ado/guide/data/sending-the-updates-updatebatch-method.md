---
title: "Enviar actualizaciones: método UpdateBatch | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cad1bfd63ffafd32d0621f6142717cd7175ccd0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sending-the-updates-updatebatch-method"></a>Enviar actualizaciones: método UpdateBatch
El código siguiente abre un conjunto de registros en modo por lotes estableciendo la propiedad LockType en adLockBatchOptimistic y CursorLocation en adUseClient. Agrega dos registros nuevos y cambia el valor de un campo en un registro existente y guarda los valores originales y, a continuación, llama al método UpdateBatch para enviar que los cambios de vuelta al origen de datos.  
  
## <a name="remarks"></a>Comentarios  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
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
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 Si está modificando el registro actual o agregando un nuevo registro cuando se llama al método UpdateBatch, ADO llamará automáticamente al método Update para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)

