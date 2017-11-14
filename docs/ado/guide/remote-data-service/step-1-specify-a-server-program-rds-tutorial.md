---
title: 'Paso 1: Especificar un programa de servidor (Tutorial RDS) | Documentos de Microsoft'
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
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c79cf47179f8fff140f4fda779b5db816c1d9418
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Paso 1: Especificar un programa de servidor (Tutorial RDS)
En el caso más general, utilice el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para especificar el programa de servidor predeterminado, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), o su propio programa de servidor personalizado (objeto comercial). Se crea una instancia de un programa de servidor en el servidor y una referencia al programa de servidor, o *proxy*, se devuelve.  
  
 Este tutorial utiliza el programa de servidor predeterminado:  
  
```  
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Paso 2: Llamar al programa de servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

