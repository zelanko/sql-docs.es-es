---
title: 'Paso 4: Rellenar el cuadro de texto detalles | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da260e3dd3006a56e0be90c2b7e0c33ed0869781
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272884"
---
# <a name="step-4-populate-the-details-text-box"></a>Paso 4: Rellenar el cuadro de texto de detalles
Para rellenar el cuadro de texto de detalles, cree una subrutina nueva denominada **recFields** e inserte el código siguiente:  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 Este código rellena `lstDetails` con los campos y valores del registro simple pasado a `recFields`. Si el recurso es un archivo de texto, una secuencia de texto se abre desde el registro de recursos. El código determina si el juego de caracteres es ASCII y copia el contenido de la secuencia en `txtDetails`.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 3: Rellenar el cuadro de lista de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
