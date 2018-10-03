---
title: Escenario de persistencia de conjunto de registros XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 252df4b5133861b6ff9892600bfe1c53206fefec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789223"
---
# <a name="xml-recordset-persistence-scenario"></a>Escenario de persistencia del conjunto de registros XML
En este escenario, creará una aplicación de páginas Active Server (ASP) que guarda el contenido de un objeto de conjunto de registros directamente en el objeto de respuesta de ASP.  
  
> [!NOTE]
>  Este escenario requiere que el servidor tiene 5.0 de Internet Information Server (IIS) o una versión posterior instalada.  
  
 El conjunto de registros devuelto se muestra en el Explorador de Internet mediante un [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md).  
  
 Los pasos siguientes son necesarios para crear este escenario:  
  
-   Configuración de la aplicación  
  
-   Obtener los datos  
  
-   Enviar los datos  
  
-   Recibir y mostrar los datos  
  
## <a name="step-1-set-up-the-application"></a>Paso 1: Configurar la aplicación  
 Cree un directorio virtual denominado "XMLPersist", con permisos de la secuencia de comandos. Cree dos nuevos archivos de texto en la carpeta a la que señala el directorio virtual, una con nombre "XMLResponse.asp," el otro denominado "Default.htm".  
  
## <a name="step-2-get-the-data"></a>Paso 2: Obtener los datos  
 En este paso, escribirá el código para abrir un conjunto de registros ADO y prepararlo para su envío al cliente. Abra el archivo XMLResponse.asp con un editor de texto como Bloc de notas e inserte el código siguiente.  
  
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
  
 No olvide cambiar el valor de la `Data Source` parámetro `strCon` en el nombre de su equipo de Microsoft SQL Server.  
  
 Mantener el archivo abierto y vaya al paso siguiente.  
  
## <a name="step-3-send-the-data"></a>Paso 3: Enviar los datos  
 Ahora que tiene un conjunto de registros, debe enviar al cliente, se almacena como XML en el objeto de respuesta de ASP. Agregue el código siguiente al final de XMLResponse.asp.  
  
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
  
 Tenga en cuenta que el objeto de respuesta de ASP se especifica como el destino para el conjunto de registros [método Save](../../../ado/reference/ado-api/save-method.md). El destino del método Save puede ser cualquier objeto que admita la interfaz IStream, como ADO [objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md), o un nombre de archivo que incluye la ruta de acceso completa que es el conjunto de registros se guarden.  
  
 Guarde y cierre XMLResponse.asp antes de pasar al paso siguiente. También copie el archivo adovbs.inc desde la carpeta de instalación de biblioteca de ADO de forma predeterminada en la misma carpeta donde guardó el archivo XMLResponse.asp.  
  
## <a name="step-4-receive-and-display-the-data"></a>Paso 4: Recibir y mostrar los datos  
 En este paso creará un archivo HTML con un embedded [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto que apunta al archivo XMLResponse.asp para obtener el conjunto de registros. Abra default.htm con un editor de texto como Bloc de notas y agregue el código siguiente. Reemplace "sqlserver" en la dirección URL con el nombre del servidor.  
  
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
  
 Cierre el archivo default.htm y guárdelo en la misma carpeta donde guardó XMLResponse.asp. Uso de Internet Explorer 4.0 o posterior, abra la dirección URL http://*sqlserver*/XMLPersist/default.htm y observe los resultados. Los datos se muestran en una tabla enlazada de DHTML. Ahora, abra la dirección URL http:// *sqlserver* /XMLPersist/XMLResponse.asp y observe los resultados. Se muestra el código XML.  
  
## <a name="see-also"></a>Vea también  
 [Save (método)](../../../ado/reference/ado-api/save-method.md)   
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
