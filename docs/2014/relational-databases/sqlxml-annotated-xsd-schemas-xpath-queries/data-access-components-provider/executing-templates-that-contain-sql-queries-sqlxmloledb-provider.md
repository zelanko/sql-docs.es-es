---
title: Ejecutar plantillas que contienen consultas SQL (proveedor SQLXMLOLEDB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- templates [SQLXML]
- SQLXMLOLEDB Provider, executing template files
- templates [SQLXML], SQL queries
- XML templates [SQLXML]
- SQL queries [SQLXML]
ms.assetid: ff2bc36f-e3fb-4d8f-8e3a-2680a39eda11
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: affea1983c83dbf3cd0a8f5ab82292f88f1cae65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104868"
---
# <a name="executing-templates-that-contain-sql-queries-sqlxmloledb-provider"></a>Ejecutar plantillas que contienen consultas SQL (proveedor SQLXMLOLEDB)
  En este ejemplo se muestra el uso de la propiedad específica del proveedor SQLXMLOLEDB ClientSideXML. En esta aplicación de ejemplo ADO del lado cliente, se ejecuta en el servidor una plantilla XML que consta de una consulta SQL.  
  
 Porque clientsidexml, propiedad está establecida en True, la instrucción SELECT sin la cláusula FOR XML se envía al servidor. El servidor ejecuta la consulta y devuelve un conjunto de filas al cliente. A continuación, el cliente aplica la transformación FOR XML al conjunto de filas y genera un documento XML.  
  
 La plantilla XML proporciona un elemento raíz único de nivel superior (\<raíz >) para el documento XML que se genera; por lo tanto, no se proporciona la propiedad de la raíz de xml.  
  
 Para ejecutar plantillas XML, se debe especificar el dialecto {5d531cb2-e6ed-11d2-b252-00c04f681b71}.  
  
> [!NOTE]  
>  En el código, debe suministrarse el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión. Además, este ejemplo especifica el uso de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para el proveedor de datos que requiere la instalación de software de cliente de red adicional. Para obtener más información, consulte [requisitos del sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
  
Sub Main()  
  Dim oTestStream As New ADODB.Stream  
  Dim oTestConnection As New ADODB.Connection  
  Dim oTestCommand As New ADODB.Command  
  oTestConnection.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
  
  Set oTestCommand.ActiveConnection = oTestConnection  
  oTestCommand.Properties("ClientSideXML") = True  
  oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:query> " & _  
        "   SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
  oTestStream.Open  
  ' You need the dialect if you are executing   
  ' XML templates (not for SQL queries).  
  oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  oTestCommand.Properties("Output Stream").Value = oTestStream  
  oTestCommand.Execute , , adExecuteStream  
  
  oTestStream.Position = 0  
  oTestStream.Charset = "utf-8"  
  Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
  
Sub Form_Load()  
  Main  
End Sub  
```  
  
  