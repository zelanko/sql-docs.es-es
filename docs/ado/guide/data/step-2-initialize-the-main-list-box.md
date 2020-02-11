---
title: 'Paso 2: inicializar el cuadro de lista principal | Microsoft Docs'
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
ms.openlocfilehash: 8ad89d806f8a6774cb0fe2de056e30fd274a517c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924084"
---
# <a name="step-2-initialize-the-main-list-box"></a>Paso 2: Inicializar el cuadro de lista principal
Para declarar los objetos de registro global y de conjunto de registros, inserte el código siguiente en (general) (declaraciones) para Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Este código declara las referencias de objeto globales para los objetos de registro y de conjunto de registros que se utilizarán más adelante en este escenario.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Para conectarse a una dirección URL y rellenar lstMain  
 Inserte el código siguiente en el controlador de eventos de carga del formulario para Form1:  
  
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
  
 Este código crea instancias del registro global y de los objetos de conjunto de registros. El objeto de registro `grec`,, se abre con una dirección URL especificada como ActiveConnection. Si la dirección URL existe, se abre; Si aún no existe, se crea. Tenga en cuenta que debe reemplazar<https://servername/foldername/>"" por una dirección URL válida de su entorno.  
  
 El objeto de conjunto `grs`de registros,, se abre en los elementos secundarios `grec`del registro,. A `lstMain` continuación, se rellena con los nombres de archivo de los recursos publicados en la dirección URL.  
  
## <a name="see-also"></a>Consulte también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 1: configurar el proyecto de Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Paso 3: Rellenar el cuadro de lista de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
