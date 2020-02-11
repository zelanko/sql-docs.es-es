---
title: 'Paso 3: rellenar el cuadro de lista campos | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d7f351b90030e755dde8ad13905ef4533eff08e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924054"
---
# <a name="step-3-populate-the-fields-list-box"></a>Paso 3: Rellenar el cuadro de lista de campos
Para rellenar el cuadro de lista campos, inserte el siguiente código en el controlador `lstMain`de eventos Click de:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 Este código declara y crea instancias de los objetos de registro local y `rec` de `rs`conjunto de registros, y, respectivamente.  
  
 La fila correspondiente al recurso seleccionado en se `lstMain` convierte en la fila actual de `grs`. A continuación, el cuadro de lista detalles `rec` está desactivado y se abre `grs` con la fila actual de como origen.  
  
 Si el recurso es un registro de colección, como se especifica en [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), se `rs` abre el conjunto de registros local en los elementos secundarios de REC. A `lstDetails` continuación, se rellena con los valores de las `rs`filas de.  
  
 Si el recurso es un registro simple, `recFields` se llama a. Para obtener más información `recFields`acerca de, vea el siguiente paso.  
  
 No se implementa ningún código si el recurso es un documento estructurado.  
  
## <a name="see-also"></a>Consulte también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 2: inicializar el cuadro de lista principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Paso 4: Rellenar el cuadro de texto de detalles](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
