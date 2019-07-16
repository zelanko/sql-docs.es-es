---
title: Detectar y resolver conflictos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce9917f144e8c63160f571a986263d8d7e97b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925562"
---
# <a name="detecting-and-resolving-conflicts"></a>Detectar y resolver conflictos
Si está trabajando con el conjunto de registros en el modo inmediato, hay mucho menos posibilidades de que se produzcan los problemas de simultaneidad. Por otro lado, si la aplicación utiliza la actualización de modo por lotes, puede haber una buena oportunidad de que un usuario cambie un registro antes de guardarán los cambios realizados por otro usuario modifica el mismo registro. En tal caso, le interesará la aplicación para controlar correctamente el conflicto. Es posible que prefiera que sea la última persona que envíe una actualización en el servidor "gana". ¿O desea permitir que el usuario más reciente para decidir qué actualizaciones deben tener prioridad, permitiéndole elegir entre los dos valores en conflicto.  
  
 En cualquier caso, ADO proporciona las propiedades UnderlyingValue y OriginalValue del objeto de campo para controlar estos tipos de conflictos. Utilice estas propiedades en combinación con el método Resync y la propiedad de filtro del conjunto de registros.  
  
## <a name="remarks"></a>Comentarios  
 Cuando ADO detecta un conflicto durante una actualización por lotes, se agregará una advertencia a la colección de errores. Por lo tanto, siempre debe comprobar si hay errores inmediatamente después de llamar a BatchUpdate y si encontrarlos, empiece por probar la suposición de que se ha producido un conflicto. El primer paso es establecer la propiedad de filtro en el conjunto de registros son iguales a adFilterConflictingRecords. Esto limita la vista en su conjunto de registros a solo aquellos registros que están en conflicto. Si la propiedad RecordCount es igual a cero después de este paso, sabrá que se produjo el error por un valor distinto de un conflicto.  
  
 Al llamar a BatchUpdate, ADO y el proveedor generan instrucciones SQL para realizar actualizaciones en el origen de datos. Recuerde que algunos orígenes de datos tienen limitaciones en el que se pueden usar tipos de columnas en una cláusula WHERE.  
  
 A continuación, llame al método Resync en el conjunto de registros con el argumento AffectRecords establecido igual a adAffectGroup y el argumento ResyncValues establecido igual a adResyncUnderlyingValues. El método Resync actualiza los datos del objeto de conjunto de registros actual de la base de datos subyacente. Si utiliza adAffectGroup, se garantiza que se vuelven a sincronizar solo los registros visibles con la configuración, es decir, solo los registros en conflicto del filtro actual con la base de datos. Esto podría suponer una diferencia significativa del rendimiento si se trata de un gran conjunto de registros. Al establecer el argumento ResyncValues en adResyncUnderlyingValues al llamar a Resync, asegúrese de que la propiedad UnderlyingValue contendrá el valor de la base de datos (en conflicto), que la propiedad Value mantendrá el valor especificado por el usuario, y que la propiedad OriginalValue contendrá el valor original del campo (el valor que tenía antes de que se realizó la última llamada correcta de UpdateBatch). A continuación, puede utilizar estos valores para resolver el conflicto mediante programación o exigir al usuario que seleccione el valor que se usará.  
  
 Esta técnica se muestra en el ejemplo de código siguiente. El ejemplo crea artificialmente un conflicto con un conjunto de registros independiente para cambiar un valor de la tabla subyacente antes de llama a UpdateBatch.  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 Puede usar la propiedad de estado del registro actual o de un campo específico para determinar qué tipo de conflicto se ha producido.  
  
 Para obtener información detallada sobre el control de errores, vea [Error Handling](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Vea también  
 [Modo por lotes](../../../ado/guide/data/batch-mode.md)
