---
title: Usar los resultados de FOR XML en el código de aplicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a8bbdb0f98dea26d73ec465d6fd9e226329345a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33017332"
---
# <a name="use-for-xml-results-in-application-code"></a>Usar los resultados de FOR XML en el código de aplicación
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Al utilizar cláusulas FOR XML con consultas SQL, se pueden recuperar e incluso convertir los resultados de la consulta como datos XML. Esta funcionalidad permite realizar las siguientes operaciones cuando los resultados de las consultas FOR XML se pueden utilizar en el código de aplicación XML:  
  
-   Consultar tablas SQL de instancias de valores de [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
-   Aplicar la [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md) para devolver como XML el resultado de las consultas que contienen datos con tipo de texto o imagen  
  
 Este tema proporciona ejemplos que muestran estos planteamientos.  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>Recuperar datos FOR XML con islas de datos ADO y XML  
 El objeto ADO **Stream** u otros objetos que admiten la interfaz COM **IStream** , como los objetos **Request** y **Response** de las páginas Active Server (ASP), se pueden usar para guardar los resultados cuando se trabaja con consultas FOR XML.  
  
 Por ejemplo, el siguiente código ASP muestra los resultados que se obtienen al consultar una columna de tipo de datos **xml** , Demographics, en la tabla Sales.Store de la base de datos de ejemplo AdventureWorks. Concretamente, la consulta busca el valor de instancia de esta columna para la fila en la que CustomerID es igual a 3.  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
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
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
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
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
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
  
 Esta página ASP de ejemplo contiene código VBScript de servidor que utiliza ADO para ejecutar la consulta FOR XML y devolver los resultados XML en una isla de datos XML, MyDataIsle. Después, la isla de datos XML se devuelve en el explorador para su posterior procesamiento del lado cliente. Después, para procesar el contenido de la isla de datos XML se utiliza código VBScript del lado cliente adicional. Este proceso se lleva a cabo antes de mostrar el contenido como parte del DHTML resultante y abrir un cuadro de mensaje con el contenido de la isla de datos XML previamente procesado.  
  
#### <a name="to-test-this-example"></a>Para probar este ejemplo  
  
1.  Compruebe que se ha instalado IIS y la base de datos de ejemplo AdventureWorks de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Este ejemplo requiere la instalación de Internet Information Services (IIS) 5.0 ó una versión posterior, con la compatibilidad con ASP habilitada. Asimismo, debe instalarse la base de datos de ejemplo AdventureWorks.  
  
2.  Copie el ejemplo de código previamente proporcionado y péguelo en su editor XML o editor de texto habitual. Guarde el archivo como RetrieveResults.asp en el directorio raíz que se utiliza para IIS. Normalmente es C:Inetpub\wwwroot.  
  
3.  Abra la página ASP en una ventana del explorador utilizando la dirección URL siguiente. Primero, sustituya "MyServer" por "localhost" o el verdadero nombre del servidor donde se han instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e IIS.  
  
    ```  
    http://MyServer/RetrieveResults.asp  
    ```  
  
 Los resultados de la página HTML generada que aparecen serán similares a la siguiente salida de ejemplo:  
  
##### <a name="server-side-processing"></a>Procesamiento en el servidor  
 Page Generated @ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI;  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 Pushing XML to client for processing  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>Procesamiento del documento XML MyDataIsle en el cliente  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 A continuación, el cuadro de mensaje VBScript mostrará el siguiente contenido de la isla de datos XML original, sin filtrar, que ha sido devuelto en los resultados de la consulta FOR XML.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>Recuperar datos FOR XML con ASP.NET y .NET Framework  
 Como en el ejemplo anterior, el siguiente código ASP.NET muestra los resultados que se obtienen al consultar una columna de tipo de datos **xml** , Demographics, en la tabla Sales.Store de la base de datos de ejemplo AdventureWorks. Como en el ejemplo anterior, la consulta busca el valor de instancia de esta columna para la fila en la que CustomerID es igual a 3.  
  
 En este ejemplo, se utilizan las siguientes API administradas de Microsoft .NET Framework para devolver y representar los resultados de la consulta FOR XML:  
  
1.  Se utiliza**SqlConnection** para abrir una conexión con SQL Server basada en el contenido de una variable de cadena de conexión especificada, strConn.  
  
2.  A continuación, se utiliza**SqlDataAdapter** como adaptador de datos y se emplea la conexión SQL y una cadena de consulta SQL especificada para ejecutar la consulta FOR XML.  
  
3.  Después de que se ha ejecutado la consulta, se llama al método **SqlDataAdapter.Fill** , al que se le pasa una instancia de **DataSet,** MyDataSet, para llenar el conjunto de datos con la salida de la consulta FOR XML.  
  
4.  Después, se llama al método **DataSet.GetXml** para devolver los resultados de la consulta como una cadena que se puede mostrar en la página HTML generada por el servidor.  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
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
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>Para probar este ejemplo  
  
1.  Compruebe que se ha instalado IIS y la base de datos de ejemplo AdventureWorks de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Este ejemplo requiere la instalación de Internet Information Services (IIS) 5.0 ó una versión posterior, con la compatibilidad con ASP.NET habilitada. Asimismo, debe instalarse la base de datos de ejemplo AdventureWorks.  
  
2.  Copie el código previamente proporcionado y péguelo en su editor XML o editor de texto habitual. Guarde el archivo como RetrieveResults.aspx en el directorio raíz utilizado para IIS. Normalmente es C:Inetpub\wwwroot.  
  
3.  Abra la página ASP.NET en una ventana del explorador utilizando la dirección URL siguiente. Primero, sustituya "MyServer" por "localhost" o el verdadero nombre del servidor donde se han instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e IIS.  
  
    ```  
    http://MyServer/RetrieveResults.aspx  
    ```  
  
 Los resultados de la página HTML generada que aparecen serán similares a la siguiente salida de ejemplo:  
  
##### <a name="server-side-processing"></a>Procesamiento en el servidor  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  La compatibilidad con el tipo de datos **xml** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite solicitar que el resultado de una consulta FOR XML se devuelva como un tipo de datos **xml** en lugar de datos con tipo cadena o imagen, especificando la [directiva TYPE](../../relational-databases/xml/type-directive-in-for-xml-queries.md). Cuando se usa la directiva TYPE en las consultas FOR XML, el tipo de acceso que se proporciona mediante programación a los resultados de FOR XML es similar al que se muestra en [Usar datos XML en las aplicaciones](../../relational-databases/xml/use-xml-data-in-applications.md).  
  
## <a name="see-also"></a>Ver también  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
