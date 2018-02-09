---
title: "Programación ADO en VBScript | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f725eec0027d1c06715b72785a1fe06a4fa4cedb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="vbscript-ado-programming"></a>Programación ADO en VBScript
## <a name="creating-an-ado-project"></a>Crear un proyecto de ADO  
 Microsoft Visual Basic Scripting Edition no admite bibliotecas de tipos, por lo que no debe hacer referencia a ADO en su proyecto. Por lo tanto, se admite ninguna característica asociada como la finalización de la línea de comandos. Además, de forma predeterminada, no se definen constantes enumeradas de ADO en VBScript.  
  
 Sin embargo, ADO proporciona que dos incluyen archivos que contienen las definiciones siguientes para su uso con VBScript:  
  
-   Para escribir secuencias de comandos de servidor, utilice Adovbs.inc, que se instala en la carpeta de programa\Archivos Files\System\ado\ c:\Program de forma predeterminada.  
  
-   Secuencias de comandos de cliente, utilice Adcvbs.inc, que se instala en la carpeta de programa\Archivos Files\System\msdac\ c:\Program de forma predeterminada.  
  
 Puede copiar y pegar las definiciones de constantes de estos archivos en sus páginas ASP o, si está realizando secuencias de comandos de servidor, copie el archivo Adovbs.inc en una carpeta en el sitio Web y hacer referencia a él desde la página ASP similar al siguiente:  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Crear objetos de ADO en VBScript  
 No se puede utilizar el **Dim** instrucción para asignar objetos a un tipo específico en VBScript. Además, VBScript no admite la **New** sintaxis utilizada con el **Dim** instrucción en Visual Basic para aplicaciones. En su lugar, debe utilizar el **CreateObject** llamada de función:  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>Ejemplos de VBScript  
 El código siguiente es un ejemplo genérico de programación de VBScript en el servidor en un archivo de página Active Server (ASP):  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 Ejemplos más específicos de VBScript se incluyen en la documentación de ADO. Para obtener más información, consulte [ejemplos de código ADO en Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md).  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Diferencias entre VBScript y Visual Basic  
 Usar ADO con VBScript es similar a usar ADO con Visual Basic en muchos sentidos, por ejemplo cómo se utiliza la sintaxis. Sin embargo, existen algunas diferencias importantes:  
  
-   VBScript admite sólo el tipo de datos Variant, que puede contener diferentes tipos de datos. Puede almacenar los datos que necesita en un tipo de datos Variant, y los datos se efectuará correctamente debido a la conversión realizada por VBScript. Se reconoce el tipo requerido por ADO y convierte el valor de la variante en consecuencia.  
  
-   No se puede utilizar **en error goto \<etiqueta >** dentro de VBScript.  
  
-   VBScript admite algunas de las funciones integradas de Visual Basic como **Msgbox**, **fecha**, y **IsNumeric**. Sin embargo, dado que VBScript es un subconjunto de Visual Basic, no todas las funciones integradas se admiten. Por ejemplo, VBScript no admite la **formato** función y las funciones de E/S de archivos.
