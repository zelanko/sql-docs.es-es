---
title: Programación ADO en VBScript | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a2b6172fdd35e98d1b4a5f1b3c6ff19293a7f81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294417"
---
# <a name="vbscript-ado-programming"></a>Programación ADO en VBScript
## <a name="creating-an-ado-project"></a>Crear un proyecto de ADO  
 Microsoft Visual Basic, Scripting Edition no admite las bibliotecas de tipos, por lo que no es necesario hacer referencia a ADO en su proyecto. Por lo tanto, se admite ninguna característica asociada como la finalización de la línea de comandos. Además, de forma predeterminada, no se definen las constantes enumeradas de ADO en VBScript.  
  
 Sin embargo, ADO ofrece que dos incluyen los archivos que contienen las siguientes definiciones para su uso con VBScript:  
  
-   Uso de scripting del lado servidor Adovbs.inc, que se instala en la carpeta de c:\Program Files\Common Files\System\ado\ de forma predeterminada.  
  
-   Scripting del lado cliente, utilice Adcvbs.inc, que se instala en la carpeta de c:\Program Files\Common Files\System\msdac\ de forma predeterminada.  
  
 Puede copiar y pegar las definiciones de constantes de estos archivos en las páginas ASP o, si va a realizar el scripting del lado servidor, copie el archivo Adovbs.inc en una carpeta en su sitio Web y hacer referencia a ella desde la página ASP similar al siguiente:  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Creación de objetos ADO en VBScript  
 No puede usar el **Dim** instrucción para asignar objetos a un tipo específico en VBScript. Además, VBScript no admite la **New** sintaxis utilizada con el **Dim** instrucción en Visual Basic para aplicaciones. En su lugar, debe usar el **CreateObject** llamada de función:  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>Ejemplos de VBScript  
 El código siguiente es un ejemplo genérico de programación de VBScript del lado servidor en un archivo de páginas Active Server (ASP):  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
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
  
 Ejemplos de VBScript más específicos se incluyen con la documentación de ADO. Para obtener más información, consulte [ejemplos de código ADO en Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md).  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Diferencias entre VBScript y Visual Basic  
 Usar ADO con VBScript es similar a usar ADO con Visual Basic de muchas maneras, incluyendo cómo se usa la sintaxis. Sin embargo, existen algunas diferencias importantes:  
  
-   VBScript la admite solo el tipo de datos Variant, lo que puede contener diferentes tipos de datos. Puede almacenar los datos que necesita en un tipo de datos Variant, y funcionan adecuadamente los datos debido a la conversión realizada por VBScript. Se reconoce el tipo requerido por ADO y convierte el valor de la variante en consecuencia.  
  
-   No puede usar **en error goto \<etiqueta >** en VBScript.  
  
-   VBScript admite algunas de las funciones integradas de Visual Basic como **Msgbox**, **fecha**, y **IsNumeric**. Sin embargo, dado que VBScript es un subconjunto de Visual Basic, no todas las funciones integradas se admiten. Por ejemplo, VBScript no admite la **formato** función y las funciones de E/S de archivos.
