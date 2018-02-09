---
title: 'Paso 2: Inicializar el cuadro de lista principal | Documentos de Microsoft'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60ece26fab2c6f691614b609d1dd3f07f42231e4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="step-2-initialize-the-main-list-box"></a>Paso 2: Inicializar el cuadro de lista principal
Para declarar objetos globales Record y conjunto de registros, inserte el código siguiente en el (General) (declaraciones) para el Form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Este código declara referencias de objetos globales para los objetos de registro y conjunto de registros que se usará más adelante en este escenario.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Para conectarse a una dirección URL y llenar lstMain  
 Inserte el código siguiente en el controlador de eventos de carga del formulario para el Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=http://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Este código crea instancias de los objetos globales Record y Recordset. El objeto de registro, `grec`, se abre con una dirección URL especificada como el objeto ActiveConnection. Si no existe la dirección URL, se abre; Si aún no existe, se crea. Tenga en cuenta que debe reemplazar "http://servername/foldername/" con una dirección URL válida de su entorno.  
  
 El objeto de conjunto de registros, `grs`, se abre sobre los elementos secundarios del registro, `grec`. A continuación, `lstMain` se rellena con los nombres de los recursos publicados en la dirección URL.  
  
## <a name="see-also"></a>Vea también  
 [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Paso 1: Configurar el proyecto de Visual Basic](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Paso 3: Rellenar el cuadro de lista de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
