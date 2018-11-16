---
title: Ejemplo de la propiedad SQL (VBScript) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- SQL property [ADO], VBScript example
ms.assetid: 32c33bcf-3320-4836-9e2e-99c8978ce581
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcfc53b0882702e5efbb53b8f88bdfb184f86df6
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601645"
---
# <a name="sql-property-example-vbscript"></a>Ejemplo de la propiedad SQL (VBScript)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 El código siguiente muestra cómo establecer el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) parámetro SQL en tiempo de diseño y enlazar a un control de datos con la base de datos denominada *Pubs*, que se incluye con Microsoft SQL Server. Para probar el ejemplo, copie el código siguiente en un documento ASP normal denominado **SQLDesignVBS.asp** en el servidor Web.  
  
```  
<!-- BeginSQLDesignVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>SQL Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>SQL Property Example (VBScript)</h1>  
  
<!-- RDS.DataControl -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDC HEIGHT=1 WIDTH=1>  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName from Employees">  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Initial Catalog='Northwind';Integrated Security='SSPI';">  
</OBJECT>  
  
<!-- Data Table -->  
  
<TABLE DATASRC=#RDC BORDER=1>  
   <TR>  
      <TD> <SPAN DATAFLD="FirstName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="LastName"></SPAN> </TD>  
   </TR>  
</TABLE>  
  
</body>  
</html>  
<!-- EndSQLDesignVBS -->  
```  
  
 El ejemplo siguiente muestra cómo establecer los parámetros necesarios de **RDS. DataControl** en tiempo de ejecución. Para probar este ejemplo, cortar y pegar el código siguiente en un documento ASP normal y asígnele el nombre **SQLRuntimeVBS.asp**. Secuencia de comandos ASP identificará el servidor.  
  
```  
<!-- BeginSQLRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>SQL Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
<h1>SQL Property Example (VBScript)</h1>  
  
<H2>RDS API Code Examples </H2>  
<H3>Remote Data Service SQL Property Set at Run Time</H3>  
  
<!-- RDS.DataControl with no parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC HEIGHT=1 WIDTH=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <SPAN DATAFLD="FirstName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="LastName"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Title"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Type"></SPAN> </TD>  
      <TD> <SPAN DATAFLD="Email"></SPAN> </TD>  
   </TR>  
</TABLE>  
  
<HR>  
<Input Size=70 Name="txtServer" Value= "https://<%=Request.ServerVariables("SERVER_NAME")%>">  
<BR>  
<Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';">  
<BR>  
<Input Size=70 Name="txtSQL" VALUE="Select * from Employees">  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
<Script Language="VBScript">  
<!--  
' Set parameters of RDS.DataControl at Run Time.  
Sub Run_OnClick  
   RDC.Server = txtServer.Value  
   RDC.SQL = txtSQL.Value  
   RDC.Connect = txtConnect.Value  
   RDC.Refresh  
End Sub  
-->  
</Script>  
  
</body>  
</html>  
<!-- EndSQLRuntimeVBS -->  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Propiedad SQL](../../../ado/reference/rds-api/sql-property.md)



