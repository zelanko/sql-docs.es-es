---
title: 'Paso 5: Control de datos es realizado utilizable (Tutorial de RDS) | Documentos de Microsoft'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f59e167dfad5ddd4b99d784b34e37556a076a2f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>Paso 5: Control de datos es realizado utilizable (Tutorial de RDS)
El valor devuelto **Recordset** objeto está disponible para su uso. Puede examinar, navegue o editarlo como lo haría con cualquier otro **conjunto de registros**. ¿Qué puede hacer con el **Recordset** depende del entorno. Visual Basic y Visual C++ poseen controles visuales que pueden usar un **Recordset** directa o indirectamente con la Ayuda de un control de datos.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por ejemplo, si se muestra una página Web en Microsoft Internet Explorer, puede mostrar el **Recordset** datos en un control visual del objeto. No se pueden obtener acceso los controles visuales de una página Web un **Recordset** objeto directamente. Sin embargo, puede tener acceso a la **Recordset** objeto a través de la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md). El **RDS. DataControl** puede ser utilizado por un objeto visual y controla cuándo su [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) propiedad está establecida en el **Recordset** objeto.  
  
 El objeto control visual debe tener su **DATASRC** parámetro establecido en el **RDS. DataControl**y su **DATAFLD** propiedad establecida en un **Recordset** campo (columna) del objeto.  
  
 En este tutorial, establezca la **SourceRecordset** propiedad:  
  
```  
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Paso 6: Los cambios se envían al servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

