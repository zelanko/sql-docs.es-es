---
title: Escenario de persistencia de conjunto de registros XML | Documentos de Microsoft
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
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd47944f218c6cb4d3bea571b27be990c5f7f530
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="xml-recordset-persistence-scenario"></a>Escenario de persistencia del conjunto de registros XML
En este escenario, creará una aplicación de páginas Active Server (ASP) que se guarda el contenido de un objeto Recordset directamente en el objeto de respuesta de ASP.  
  
> [!NOTE]
>  Este escenario requiere que el servidor tiene servicios de Internet Information Server 5.0 (IIS) o posterior instalado.  
  
 El conjunto de registros devuelto se muestra en Internet Explorer mediante una [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md).  
  
 Los siguientes pasos son necesarios para crear este escenario:  
  
-   Configurar la aplicación  
  
-   Obtener los datos  
  
-   Enviar los datos  
  
-   Recibir y mostrar los datos  
  
## <a name="step-1-set-up-the-application"></a>Paso 1: Configurar la aplicación  
 Cree un directorio virtual de IIS denominado "XMLPersist", con permisos de secuencia de comandos. Cree dos nuevos archivos de texto en la carpeta a la que señala el directorio virtual, uno con nombre "XMLResponse.asp" el otro denominado "Default.htm".  
  
## <a name="step-2-get-the-data"></a>Paso 2: Obtener los datos  
 En este paso, escribirá el código para abrir un conjunto de registros ADO y prepararlo para su envío al cliente. Abra el archivo XMLResponse.asp con un editor de texto, como el Bloc de notas e inserte el código siguiente.  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 No olvide cambiar el valor de la `Data Source` parámetro en `strCon` en el nombre del equipo con Microsoft SQL Server.  
  
 Mantener el archivo abierto y vaya al paso siguiente.  
  
## <a name="step-3-send-the-data"></a>Paso 3: Enviar los datos  
 Ahora que tiene un conjunto de registros, debe enviar al cliente guardándolo como XML en el objeto Response de ASP. Agregue el código siguiente al final de XMLResponse.asp.  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 Tenga en cuenta que el objeto Response de ASP se especifica como el destino para el conjunto de registros [método Save](../../../ado/reference/ado-api/save-method.md). El destino del método Save puede ser cualquier objeto que admita la interfaz IStream, como ADO [secuencia ADO (objetos)](../../../ado/reference/ado-api/stream-object-ado.md), o un nombre de archivo que incluye la ruta de acceso completa a la que es el conjunto de registros se guarden.  
  
 Guarde y cierre XMLResponse.asp antes de ir al paso siguiente. También, copie el archivo adovbs.inc de la carpeta de instalación de biblioteca de ADO de forma predeterminada en la misma carpeta donde guardó el archivo XMLResponse.asp.  
  
## <a name="step-4-receive-and-display-the-data"></a>Paso 4: Recibir y mostrar los datos  
 En este paso creará un archivo HTML con un incrustado [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto que apunta al archivo XMLResponse.asp para obtener el conjunto de registros. Abra default.htm con un editor de texto, como el Bloc de notas y agregue el código siguiente. Reemplace "sqlserver" en la dirección URL con el nombre del servidor.  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 Cierre el archivo default.htm y guárdelo en la misma carpeta donde guardó XMLResponse.asp. Usa Internet Explorer 4.0 o una versión posterior, abra la dirección URL http://*sqlserver*/XMLPersist/default.htm y observe los resultados. Los datos se muestran en una tabla DHTML enlazada. Ahora, abra la dirección URL http:// *sqlserver* /XMLPersist/XMLResponse.asp y observe los resultados. Se muestra el código XML.  
  
## <a name="see-also"></a>Vea también  
 [Save (método)](../../../ado/reference/ado-api/save-method.md)   
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)

