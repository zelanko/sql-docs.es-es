---
title: Ejemplo de la propiedad ReadyState (VBScript) | Documentos de Microsoft
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ReadyState property [ADO], VBScript example
ms.assetid: e3e18da4-0511-4ece-a35d-699978bc28c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30d015d40052b781babc865a099726d1cddd4688
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288484"
---
# <a name="readystate-property-example-vbscript"></a>Ejemplo de la propiedad ReadyState (VBScript)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 En el ejemplo siguiente se muestra cómo leer el [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) propiedad de la [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto en tiempo de ejecución en código VBScript. **ReadyState** es una propiedad de solo lectura.  
  
 Para probar este ejemplo, corte y pegue este código entre las \<cuerpo > y \</cuerpo > etiquetas en una HTML normal de documento y asígnele el nombre **RDSReadySt.asp**. Usar **buscar** para localizar el archivo Adovbs.inc y colocarlo en el directorio que se va a utilizar. Secuencia de comandos ASP identificará el servidor.  
  
```  
<!-- BeginReadyStateVBS -->  
<%@ Language=VBScript %>  
<!--#include file="adovbs.inc"-->  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>RDS.DataControl ReadyState Property</title>  
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
<H1>RDS.DataControl ReadyState Property</H1>  
<H2>RDS API Code Examples </H2>  
<HR>  
<!-- RDS.DataControl with parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS>  
   <PARAM NAME="SQL" VALUE="Select * from Orders">  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Integrated Security=SSPI;Initial Catalog=Northwind">  
   <PARAM NAME="ExecuteOptions" VALUE="2">   
   <PARAM NAME="FetchOptions" VALUE="3">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="OrderID"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<Script Language="VBScript">  
  
   Sub Window_OnLoad  
  
      Select Case RDS.ReadyState  
         case 2   'adcReadyStateLoaded  
          MsgBox "Executing Query"  
         case 3   'adcReadyStateInteractive  
          MsgBox "Fetching records in background"  
         case 4   'adcReadyStateComplete  
          MsgBox "All records fetched"  
      End Select  
  
   End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndReadyStateVBS -->  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Propiedad ReadyState (RDS)](../../../ado/reference/rds-api/readystate-property-rds.md)


