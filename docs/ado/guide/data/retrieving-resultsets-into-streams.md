---
title: Recuperar conjuntos de resultados en secuencias | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45ba231b1523a74ac8b2c09f55e19c3dc287ef20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734963"
---
# <a name="retrieving-resultsets-into-streams"></a>Recuperar conjuntos de resultados en secuencias
En lugar de recibir los resultados en el tradicional **Recordset** objeto ADO en su lugar, puede recuperar los resultados de la consulta en una secuencia. ADO **Stream** objeto (u otros objetos que admiten el COM **IStream** interfaz, por ejemplo, el ASP **solicitar** y **respuesta** objetos ) se puede usar para contener estos resultados. Un uso de esta característica es para recuperar los resultados en formato XML. Con SQL Server, por ejemplo, los resultados XML pueden devolverse de varias formas, por ejemplo, mediante la cláusula FOR XML con una consulta SELECT de SQL o mediante una consulta XPath.  
  
 Para recibir los resultados de la consulta en formato de secuencia en lugar de en un **Recordset**, debe especificar el **adExecuteStream** constante desde **ExecuteOptionEnum** como un parámetro de la **Execute** método de un **comando** objeto. Si su proveedor admite esta característica, se devolverá los resultados en una secuencia en la ejecución. Podría ser necesario para especificar propiedades específicas del proveedor adicionales antes de que se ejecuta el código. Por ejemplo, con el proveedor Microsoft OLE DB para SQL Server, propiedades, como **salida Stream** en el **propiedades** colección de la **comando** objeto debe ser especificado. Para obtener más información acerca de propiedades dinámicas específicas de SQL Server relacionado con esta característica, vea las propiedades de XML-Related en los libros en pantalla de SQL Server.  
  
## <a name="for-xml-query-example"></a>Por ejemplo de consulta XML  
 En el siguiente ejemplo está escrito en VBScript a la base de datos Northwind:  
  
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
  
### <a name="for-xml-syntax"></a>Para conocer la sintaxis XML  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 PARA XML sin formato genera los elementos de fila genérico que tienen valores de columna como atributos. FOR XML AUTO utiliza la heurística para generar un árbol jerárquico con nombres de elementos en función de los nombres de tabla. FOR XML EXPLICIT genera una tabla universal con relaciones que se describen con detalle mediante metadatos.  
  
 Un instrucción SQL SELECT FOR XML de ejemplo:  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 El comando se puede especificar en una cadena, como se mostró anteriormente, asignado a **CommandText**, o en forma de una consulta de la plantilla XML asignada a **CommandStream**. Para obtener más información acerca de las consultas de plantilla XML, vea [secuencias de comandos](../../../ado/guide/data/command-streams.md) en ADO o mediante secuencias de entrada de comando en los libros en pantalla de SQL Server.  
  
 Como una consulta de la plantilla XML, la consulta FOR XML aparece como sigue:  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 Este ejemplo especifica el ASP **respuesta** de objeto para el **salida Stream** propiedad:  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 A continuación, especifique **adExecuteStream** parámetro de **Execute**. Este ejemplo ajusta la secuencia de etiquetas XML para crear una isla de datos XML:  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>Comentarios  
 En este momento, XML ha sido transmitido al explorador del cliente y está listo para ser mostrado. Esto se realiza mediante VBScript del lado cliente para enlazar el documento XML a una instancia de DOM y crear bucles en cada nodo secundario para crear una lista de productos en HTML.
