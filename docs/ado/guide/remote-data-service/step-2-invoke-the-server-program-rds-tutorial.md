---
title: 'Paso 2: Invocar el programa de servidor (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a2e7b62276234dcf11067395ff2512a8e93af96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800513"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Paso 2: invocar un programa de servidor (Tutorial de RDS)
Cuando se invoca un método en el cliente *proxy*, el programa real en el servidor ejecuta el método. En este paso, deberá ejecutar una consulta en el servidor.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Parte A** si no usara [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) en este tutorial, la manera más conveniente para realizar este paso sería usar la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto. El **RDS. DataControl** combina el paso de creación de un proxy, con este paso, emita la consulta anterior.  
  
 Establecer el **RDS. DataControl** objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propiedad para identificar dónde se debe crear una instancia el programa del servidor; el [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propiedad para especificar la cadena de conexión para tener acceso al origen de datos; y el [SQL](../../../ado/reference/rds-api/sql-property.md) propiedad para especificar el texto del comando de consulta. A continuación, emita el [actualizar](../../../ado/reference/rds-api/refresh-method-rds.md) método hace que el programa de servidor para conectarse al origen de datos, recupere las filas especificadas por la consulta y devolver un **Recordset** objeto al cliente.  
  
 En este tutorial no utiliza el **RDS. DataControl**, pero se trata cómo aparecería si lo hiciera:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Ni invoca el tutorial de RDS con objetos ADO, pero se trata de cómo sería si lo hiciera:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **La parte B** es el método general para realizar este paso invocar el **RDSServer.DataFactory** objeto [consulta](../../../ado/reference/rds-api/query-method-rds.md) método. Ese método toma una cadena de conexión, que se usa para conectarse a un origen de datos, y un texto de comando, que se usa para especificar las filas que se va a devolver desde el origen de datos.  
  
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
 [Paso 3: El servidor obtiene un conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
