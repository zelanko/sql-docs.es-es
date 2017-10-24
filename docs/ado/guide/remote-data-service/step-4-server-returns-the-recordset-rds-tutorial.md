---
title: 'Paso 4: El servidor devuelve el conjunto de registros (Tutorial RDS) | Documentos de Microsoft'
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1cc20f813b87432ede6f0ecf98cd1dd41bd526fd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>Paso 4: El servidor devuelve el conjunto de registros (Tutorial RDS)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS convierte el objeto recuperado **conjunto de registros** objeto a un formulario que se pueden enviar al cliente (es decir, se *calcula* el **conjunto de registros**). La forma exacta de la conversión y la forma en se envía depende de si el servidor está en Internet o una intranet, una red de área local, o es una biblioteca de vínculos dinámicos. Sin embargo, este detalle no es crítico; todos los que es importante es que RDS envía el **Recordset** al cliente.  
  
 En el lado del cliente, un **Recordset** objeto se devuelve y se asigna a una variable local.  
  
```  
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Paso 5: Control de datos es realizado utilizable (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

