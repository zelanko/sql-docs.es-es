---
title: Uso de un objeto de conexión | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e04067cda6fad31ebd07f5d887e387139c7739b1
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979777"
---
# <a name="using-a-connection-object"></a>Uso de un objeto de conexión
Antes de abrir un **conexión** objeto, debe definir cierta información sobre el origen de datos y el tipo de conexión. La mayor parte de esta información se mantiene por el *ConnectionString* parámetro de la [método Open](../../../ado/reference/ado-api/open-method-ado-connection.md) en el **conexión** objeto, o mediante el [ConnectionString propiedad](../../../ado/reference/ado-api/connectionstring-property-ado.md) en el **conexión** objeto. Una cadena de conexión consta de una lista de pares de argumento y valor separados por punto y coma, con los valores entre comillas simples. Por ejemplo:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  También puede especificar un nombre de origen de datos ODBC (DSN) o un archivo de Data Link (UDL) en una cadena de conexión. Para obtener más información acerca de los DSN, vea [administrar orígenes de datos](../../../odbc/admin/managing-data-sources.md) en referencia del programador de ODBC. Para obtener más información acerca de los UDL, vea [Introducción a la API de vínculo de datos](http://msdn.microsoft.com/95c180ea-bd4f-4dca-b95a-576afd135bbc) en referencia de la base de datos del programador de OLE.  
  
 Por lo general, establecer una conexión mediante una llamada a la **Connection.Open** método con un adecuado un *cadena de conexión* como su parámetro. En el siguiente fragmento de código de Visual Basic se muestra un ejemplo:  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 Aquí **oRs.Open** toma un **conexión** objeto (*oConn*) variable como el valor de su *ActiveConnection* parámetro. Además, el **Connection.CursorLocation** propiedad supone el valor predeterminado de **adUseServer**. Compare esto con el [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) ejemplo en la sección anterior. La siguiente instrucción daría lugar a errores en tiempo de ejecución.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
