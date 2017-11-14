---
title: "Paso 6: Los cambios se envían al servidor (Tutorial de RDS) | Documentos de Microsoft"
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
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b811d4b5fb1809c0e528f644f28d81559d5df6b6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>Paso 6: Los cambios se envían al servidor (Tutorial de RDS)
Si el **Recordset** se edita el objeto, cualquier cambio (es decir, las filas que se agregan, cambian o eliminan) puede enviarse al servidor.  
  
> [!NOTE]
>  El comportamiento predeterminado de RDS se puede invocar implícitamente con objetos ADO y el proveedor de servicios remotos de Microsoft OLE DB. Las consultas pueden devolver **Recordset**s y editado **Recordset**s puede actualizar el origen de datos. Este tutorial no utiliza RDS con objetos ADO, pero se trata cómo aparecería si lo hiciera:  
  
```  
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=http://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **Parte A** suponga para este caso que sólo ha utilizado el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) y que un **Recordset** objeto está asociado con el **RDS. DataControl**. El [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) método actualiza el origen de datos con los cambios realizados en el **Recordset** objeto si el [Server](../../../ado/reference/rds-api/server-property-rds.md) y [conectar](../../../ado/reference/rds-api/connect-property-rds.md) todavía se establecen propiedades.  
  
```  
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "http://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **La parte B** o bien, puede actualizar el servidor con el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto Database, especificando una conexión y un **Recordset** objeto.  
  
```  
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **Éste es el final del tutorial.**  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Proveedor de servicios remotos de Microsoft OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

