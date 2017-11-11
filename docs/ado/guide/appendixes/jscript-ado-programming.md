---
title: "Programación ADO con JScript | Documentos de Microsoft"
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
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ae8137c2e5641594c3ddcf768c47b7fe844fafc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="jscript-ado-programming"></a>Programación ADO con JScript
## <a name="creating-an-ado-project"></a>Crear un proyecto de ADO  
 Microsoft JScript no admite las bibliotecas de tipos, por lo que no es necesario hacer referencia a ADO en su proyecto. Por lo tanto, se admite ninguna característica asociada como la finalización de la línea de comandos. Además, de forma predeterminada, no se definen constantes enumeradas de ADO en JScript.  
  
 Sin embargo, ADO proporciona que dos incluyen archivos que contienen las definiciones siguientes para su uso con JScript:  
  
-   Para escribir secuencias de comandos de servidor, utilice Adojavas.inc, que se instala en las carpetas de la biblioteca de ADO.  
  
-   Para escribir secuencias de comandos de cliente, utilice Adcjavas.inc, que se instala en las carpetas de la biblioteca de ADO.  
  
 Puede copiar y pegar las definiciones de constantes de estos archivos en sus páginas ASP o, si está realizando secuencias de comandos de servidor, copie el archivo Adojavas.inc en una carpeta en el sitio Web y hace referencia a él desde la página ASP similar al siguiente:  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Crear objetos de ADO en JScript  
 En su lugar, debe utilizar el **CreateObject** llamada de función:  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Ejemplo de JScript  
 El código siguiente es un ejemplo genérico de programación de servidor con JScript en un archivo de página Active Server (ASP) que se abre un **Recordset** objeto:  
  
```  
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```

