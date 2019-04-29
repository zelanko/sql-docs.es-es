---
title: 'Paso 3: Rellenar el cuadro de lista de campos | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 1aecb94fd7367b12ed2c1aaca06ffe26f586e604
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062781"
---
# <a name="step-3-populate-the-fields-list-box"></a>Paso 3: Relleno del cuadro de lista de campos
Para rellenar el cuadro de lista de campos, inserte el código siguiente en el controlador de eventos Click de `lstMain`:  
  
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
  
 Este código declara y crea instancias de objetos de conjunto de registros y de registro locales, `rec` y `rs`, respectivamente.  
  
 La fila correspondiente al recurso seleccionado en `lstMain` se realiza la fila actual de `grs`. A continuación, se borra el cuadro de lista de detalles y `rec` se abre con la fila actual de `grs` como el origen.  
  
 Si el recurso es un registro de la colección, según lo especificado por [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), el conjunto de registros local `rs` se abre en los elementos secundarios de rec. A continuación, `lstDetails` se rellena con los valores de las filas de `rs`.  
  
 Si el recurso es un registro simple, `recFields` se llama. Para obtener más información sobre `recFields`, vea el paso siguiente.  
  
 Si el recurso es un documento estructurado, se implementa ningún código.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 2: Inicializar el cuadro de lista principal](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Paso 4: Rellenar el cuadro de texto de detalles](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
