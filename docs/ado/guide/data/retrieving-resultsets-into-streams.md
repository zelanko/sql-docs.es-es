---
title: Recuperar conjuntos de resultados en secuencias | Documentos de Microsoft
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
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aadb2a81cc93effa0c280f5f74e6403c7403756
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-resultsets-into-streams"></a>Recuperar conjuntos de resultados en secuencias
En lugar de recibir los resultados en tradicional **Recordset** objeto ADO en su lugar, puede recuperar los resultados de la consulta en una secuencia. La propiedad ADO **flujo** objeto (u otros objetos que admiten el COM **IStream** interfaz, como ASP **solicitar** y **respuesta** objetos ) puede usarse para contener estos resultados. Un uso de esta característica es para recuperar los resultados en formato XML. Con SQL Server, por ejemplo, los resultados XML pueden devolverse de varias maneras, por ejemplo, mediante la cláusula FOR XML con una consulta SELECT de SQL o utilizando una consulta XPath.  
  
 Para recibir los resultados de la consulta en formato de flujo en lugar de en un **Recordset**, debe especificar el **adExecuteStream** constante de **ExecuteOptionEnum** como un parámetro de la **Execute** método de un **comando** objeto. Si su proveedor admite esta característica, se devuelven los resultados en una secuencia en la ejecución. Podría ser necesaria para especificar otras propiedades específicas del proveedor antes de que se ejecuta el código. Por ejemplo, con el proveedor Microsoft OLE DB para SQL Server, propiedades como **flujo de salida** en el **propiedades** colección de la **comando** objeto debe ser especificado. Para obtener más información acerca de propiedades dinámicas específicas de SQL Server relacionado con esta característica, vea Propiedades de XML-Related en los libros en pantalla de SQL Server.  
  
## <a name="for-xml-query-example"></a>Por ejemplo, consulta XML  
 En el siguiente ejemplo se escribe en VBScript en la base de datos de Northwind:  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 La cláusula FOR XML indica a SQL Server para devolver los datos en forma de un documento XML.  
  
### <a name="for-xml-syntax"></a>Para consultar la sintaxis XML  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 PARA XML sin formato genera los elementos de fila genérico que tienen valores de columna como atributos. FOR XML AUTO usa la heurística para generar un árbol jerárquico con los nombres de los elementos en función de los nombres de tabla. FOR XML EXPLICIT genera una tabla universal con relaciones que se describen con detalle mediante metadatos.  
  
 Un instrucción SQL SELECT FOR XML de ejemplo siguiente:  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 El comando puede especificarse en una cadena, como se muestra anteriormente, se asignaron a **CommandText**, o en forma de una consulta de plantilla XML asignada a **CommandStream**. Para obtener más información acerca de las consultas de plantilla XML, vea [secuencias de comandos](../../../ado/guide/data/command-streams.md) en ADO o secuencias de uso para la entrada de comando en los libros en pantalla de SQL Server.  
  
 Como una consulta de la plantilla XML, la consulta FOR XML aparece como sigue:  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Este ejemplo especifica el ASP **respuesta** de objeto para el **flujo de salida** propiedad:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 A continuación, especifique **adExecuteStream** parámetro de **Execute**. Este ejemplo ajusta la secuencia en etiquetas XML para crear una isla de datos XML:  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Comentarios  
 En este momento, se han transmitido por secuencias XML en el explorador del cliente y está listo para mostrarse. Esto se realiza mediante VBScript del lado cliente para enlazar el documento XML a una instancia de DOM y crear bucles en cada nodo secundario para generar una lista de productos en HTML.

