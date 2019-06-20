---
title: 'Paso 2: Inicializar el cuadro de lista principal | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0df631ccaa9cd3a6177cb4e4e8e63c65286ad361
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700365"
---
# <a name="step-2-initialize-the-main-list-box"></a>Paso 2: Inicialización del cuadro de lista principal
Para declarar objetos globales de registro y el conjunto de registros, inserte el código siguiente en el (General) (declaraciones) para el Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Este código declara referencias de objetos globales para los objetos de registro y el conjunto de registros que se usará más adelante en este escenario.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Para conectarse a una dirección URL y llenar lstMain  
 Inserte el código siguiente en el controlador de eventos Form Load para Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Este código crea instancias de los objetos globales de registro y el conjunto de registros. El objeto de registro, `grec`, se abre con una dirección URL especificada como ActiveConnection. Si no existe la dirección URL, se abre; Si no existe, se crea. Tenga en cuenta que debe reemplazar "<https://servername/foldername/>" con una dirección URL válida de su entorno.  
  
 El objeto Recordset, `grs`, se abre en los elementos secundarios del registro, `grec`. A continuación, `lstMain` se rellena con los nombres de los recursos publicados en la dirección URL.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 1: Configurar el proyecto de Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Paso 3: Rellenar el cuadro de lista de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
