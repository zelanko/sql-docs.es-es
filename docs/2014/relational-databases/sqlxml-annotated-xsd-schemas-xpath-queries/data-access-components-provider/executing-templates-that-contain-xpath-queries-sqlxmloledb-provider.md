---
title: Ejecutar plantillas que contienen consultas XPath (proveedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing template files
- Base Path property
- templates [SQLXML], XPath queries
- XPath queries [SQLXML], templates
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- Mapping Schema property
- XML templates [SQLXML]
ms.assetid: 7368c188-607e-459e-8254-8f23352dfa01
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 86008aa37f45321b7527014a640d176423d6f194
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856540"
---
# <a name="executing-templates-that-contain-xpath-queries-sqlxmloledb-provider"></a>Ejecutar plantillas que contienen consultas XPath (Proveedor SQLXMLOLEDB)
  En este ejemplo se muestra cómo utilizar las siguientes propiedades SQLXMLOLEDB específicas del proveedor:  
  
-   ClientSideXML  
  
-   Ruta de acceso base  
  
-   Esquema de asignación  
  
 En esta aplicación ADO de ejemplo, se especifica una plantilla XML que consta de una consulta de XPath (raíz) en el esquema de asignación XSD (MySchema.xml) que se describe en [ejecutar consultas XPath &#40;proveedor SQLXMLOLEDB&#41; ](executing-xpath-queries-sqlxmloledb-provider.md).  
  
 La propiedad de esquema de asignación proporciona el esquema de asignación XSD en el que se ejecuta la consulta XPath. La propiedad de ruta de acceso Base proporciona la ruta de acceso al esquema de asignación.  
  
 El clientsidexml, propiedad se establece en True. Por lo tanto, el documento XML se genera en el cliente.  
  
 En la aplicación, se especifica una consulta XPath directamente. Por lo tanto, debe estar incluido el lenguaje {5d531cb2-e6ed-11d2-b252-00c04f681b71}.  
  
> [!NOTE]  
>  En el código, debe proporcionar el nombre de la instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión. Además, este ejemplo especifica el uso de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para el proveedor de datos que requiere el software de cliente de red adicional para instalarse. Para obtener más información, consulte [requisitos del sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Sub Main()  
  
   Dim oTestStream As New ADODB.Stream  
   Dim oTestConnection As New ADODB.Connection  
   Dim oTestCommand As New ADODB.Command  
  
   oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
  
   oTestCommand.ActiveConnection = oTestConnection  
   oTestCommand.Properties("ClientSideXML") = "False"  
  
   oTestCommand.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'> " & _  
        " <sql:xpath-query mapping-schema='mySchema.xml' > " & _  
        "   root " & _  
        "   </sql:xpath-query> " & _  
        " </ROOT> "  
   oTestStream.Open  
   ' You need the dialect if you are executing a template.  
   oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
   oTestCommand.Properties("Output Stream").Value = oTestStream  
   oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\TemplateWithXPath\"  
   oTestCommand.Properties("Mapping Schema").Value = "mySchema.xml"  
   oTestCommand.Properties("Output Encoding") = "utf-8"  
   oTestCommand.Execute , , adExecuteStream  
   oTestStream.Position = 0  
   oTestStream.Charset = "utf-8"  
   Debug.Print oTestStream.ReadText(adReadAll)  
  
End Sub  
  
Sub Form_Load()  
   Main  
End Sub  
```  
  
 Éste es el esquema:  
  
```  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
   xmlns:sql='urn:schemas-microsoft-com:mapping-schema'>  
 <xsd:element name= 'root' sql:is-constant='1'>   
    <xsd:complexType>  
       <xsd:sequence>  
         <xsd:element ref = 'Contact'/>  
       </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
  
  <xsd:element name='Contact' sql:relation='Person.Contact'>  
     <xsd:complexType>  
          <xsd:attribute name='ContactID' type='xsd:integer' />  
          <xsd:attribute name='FirstName' type='xsd:string'/>   
          <xsd:attribute name='LastName' type='xsd:string' />   
     </xsd:complexType>  
   </xsd:element>  
</xsd:schema>  
```  
  
  
