---
title: Ejecutar consultas SQL (proveedor SQLXMLOLEDB)
description: Obtenga información acerca de cómo usar las propiedades de Clientsidexml, y raíz XML del proveedor SQLXMLOLEDB al ejecutar una consulta SQL del lado cliente.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXMLOLEDB Provider
- xml root property [SQLXML]
- SQLXMLOLEDB Provider, executing SQL queries
- SQL queries [SQLXML]
ms.assetid: 50334cf5-9c87-4c00-9beb-e08577c4fa82
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ad97db8811bf62342963f95fbf5feb3951c4d9c0
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882457"
---
# <a name="executing-sql-queries-sqlxmloledb-provider"></a>Ejecutar consultas SQL (proveedor SQLXMLOLEDB)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este ejemplo se muestra el uso de las siguientes propiedades SQLXMLOLEDB específicas del proveedor:  
  
-   Clientsidexml,  
  
-   xml root  
  
 En esta aplicación de ejemplo ADO del lado cliente, se ejecuta una consulta SQL simple en el cliente. Dado que la propiedad Clientsidexml, está establecida en true, la instrucción SELECT sin la cláusula FOR XML se envía al servidor. El servidor ejecuta la consulta y devuelve un conjunto de filas al cliente. A continuación, el cliente aplica la transformación FOR XML al conjunto de filas y genera un documento XML.  
  
 La propiedad raíz XML proporciona el elemento raíz de nivel superior único para el documento XML que se genera.  
  
> [!NOTE]  
>  En el código, debe proporcionar el nombre de la instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión. Además, este ejemplo especifica el uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para el proveedor de datos, que exige la instalación de software cliente de red adicional. Para obtener más información, vea [requisitos del sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI ;"  
oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = "SELECT TOP 10 FirstName, LastName FROM Person.Contact FOR XML AUTO"  
oTestStream.Open  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("xml root") = "root"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
  
