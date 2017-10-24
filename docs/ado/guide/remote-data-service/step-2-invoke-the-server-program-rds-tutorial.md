---
title: 'Paso 2: Llamar al programa de servidor (Tutorial RDS) | Documentos de Microsoft'
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
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd6ffeef7f178c7823b25fcd9a6b8e1a73c6756b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Paso 2: Llamar al programa de servidor (Tutorial RDS)
Cuando se invoca un método en el cliente *proxy*, el programa real en el servidor ejecuta el método. En este paso, deberá ejecutar una consulta en el servidor.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Parte A** si no usa [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) en este tutorial, la manera más conveniente para realizar este paso sería utilizar el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto. El **RDS. DataControl** combina el paso anterior de crear un proxy con este paso, emita la consulta.  
  
 Establecer el **RDS. DataControl** objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propiedad para identificar a donde el programa de servidor se debería crear instancias; el [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad para especificar la cadena de conexión para tener acceso al origen de datos; y el [SQL](../../../ado/reference/rds-api/sql-property.md) propiedad para especificar el texto del comando de consulta. A continuación, emita el [actualizar](../../../ado/reference/rds-api/refresh-method-rds.md) método para que el programa de servidor para conectarse al origen de datos, recupere las filas especificadas por la consulta y devolver un **Recordset** objeto al cliente.  
  
 Este tutorial no utiliza el **RDS. DataControl**, pero se trata cómo aparecería si lo hiciera:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Ni el tutorial utiliza RDS con objetos ADO, pero se trata cómo aparecería si lo hiciera:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **La parte B** es el método general para realizar este paso invocar la **RDSServer.DataFactory** objeto [consulta](../../../ado/reference/rds-api/query-method-rds.md) método. Ese método toma una cadena de conexión, que se utiliza para conectarse a un origen de datos, y un texto de comando, que se utiliza para especificar las filas que se devuelven desde el origen de datos.  
  
 Este tutorial se usa el **DataFactory** objeto **consulta** método:  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Paso 3: El servidor obtiene un conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

