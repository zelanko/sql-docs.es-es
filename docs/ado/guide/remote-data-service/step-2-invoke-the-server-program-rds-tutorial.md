---
description: 'Paso 2: Invocación de un programa de servidor (Tutorial de RDS)'
title: 'Paso 2: invocar el programa de servidor (tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b864578b67eda29c703bcf4952a9a2878aafe9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451947"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Paso 2: Invocación de un programa de servidor (Tutorial de RDS)
Al invocar un método en el *proxy*de cliente, el programa real del servidor ejecuta el método. En este paso, ejecutará una consulta en el servidor.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Parte A** Si no usa [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) en este tutorial, la forma más cómoda de realizar este paso sería usar [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) . **Objeto RDS. DataControl** combina el paso anterior para crear un proxy, con este paso, que emite la consulta.  
  
 Establezca el **objeto RDS. ** Propiedad del [servidor](../../../ado/reference/rds-api/server-property-rds.md) de objetos DataControl para identificar el lugar en el que se debe crear una instancia del programa de servidor; la propiedad [Connect](../../../ado/reference/rds-api/connect-property-rds.md) para especificar la cadena de conexión para tener acceso al origen de datos; y la propiedad [SQL](../../../ado/reference/rds-api/sql-property.md) para especificar el texto del comando de consulta. A continuación, emita el método [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md) para que el programa de servidor se conecte al origen de datos, recupere las filas especificadas por la consulta y devuelva un objeto de **conjunto de registros** al cliente.  
  
 En este tutorial no se utiliza **RDS. DataControl**, pero este es el aspecto que tendría:  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Tampoco invoca RDS con objetos ADO, pero así es como sería si lo hiciera:  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **Parte B** El método general para realizar este paso consiste en invocar el método de [consulta](../../../ado/reference/rds-api/query-method-rds.md) de objeto **RDSServer. DataFactory** . Ese método toma una cadena de conexión, que se utiliza para conectarse a un origen de datos, y un texto de comando, que se usa para especificar las filas que se van a devolver desde el origen de datos.  
  
 En este tutorial se usa el método de **consulta** de objeto **DataFactory** :  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte también  
 [Paso 3: el servidor obtiene un conjunto de registros (tutorial de RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
