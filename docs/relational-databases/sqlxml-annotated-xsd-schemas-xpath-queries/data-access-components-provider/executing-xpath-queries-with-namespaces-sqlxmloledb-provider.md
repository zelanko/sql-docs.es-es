---
title: Ejecutar consultas XPath con espacios de nombres (proveedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing XPath queries
- namespaces property
- queries [SQLXML], SQLXMLOLEDB Provider
- XPath queries [SQLXML], namespaces
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- namespaces [SQLXML], XPath queries
ms.assetid: 024a4b7d-435d-47ba-9e80-2c2f640108f5
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 28e2b2a5cd52e6881be8bda663cb8989a2e12496
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43059731"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxmloledb-provider"></a>Ejecutar consultas XPath con espacios de nombres (proveedor SQLXMLOLEDB)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Las consultas XPath pueden incluir espacios de nombres. Si los elementos de esquema son espacios de nombres calificados (es decir, si incluyen un espacio de nombres de destino), las consultas XPath que se realicen en el esquema deben especificar este espacio de nombres.  
  
 Dado que no se admite el uso del carácter comodín (*) en SQLXML 4.0, la consulta XPath debe especificarse utilizando un prefijo de espacio de nombres. Para resolver este prefijo, utilice la propiedad de los espacios de nombres para especificar el enlace de espacio de nombres.  
  
 En el ejemplo siguiente, la consulta XPath especifica los espacios de nombres con el carácter comodín (\*) y las funciones de XPath local-name() y espacio. Esta consulta XPath devuelve todos los elementos donde el nombre local es **póngase en contacto con** y el espacio de nombres URI es **urn: myschema:Contacts**.  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 En SQLXML 4.0, esta consulta XPath debe especificarse con un prefijo de espacio de nombres. Un ejemplo es **x: contacto**, donde **x** es el prefijo de espacio de nombres. Fíjese en el siguiente esquema XSD:  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 Dado que en este esquema se define el espacio de nombres de destino, una consulta XPath (como "Employee") en el esquema debe incluir el espacio de nombres.  
  
 Se trata de una aplicación [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic de ejemplo que ejecuta una consulta XPath (x:Employee) en el esquema XSD anterior. Para resolver el prefijo, el enlace de espacio de nombres se especifica mediante la propiedad de los espacios de nombres.  
  
> [!NOTE]  
>  En el código, debe suministrarse el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión. Además, este ejemplo especifica el uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para el proveedor de datos, que exige la instalación de software cliente de red adicional. Para obtener más información, consulte [requisitos del sistema para SQL Server Native Client](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Private Sub Form_Load()  
    Dim con As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim stm As New ADODB.Stream  
    con.Open "provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
    Set cmd.ActiveConnection = con  
    stm.Open  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    cmd.Properties("Mapping schema") = "C:\DirectoryPath\con-ex.xml"  
    cmd.Properties("namespaces") = "xmlns:x='urn:myschema:Contacts'"  
    '  Debug.Print "Set Command Dialect to DBGUID_XPATH"  
    cmd.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
    cmd.CommandText = "x:Contact"  
    cmd.Execute , , adExecuteStream   
    stm.Position = 0  
    Debug.Print stm.ReadText(adReadAll)  
End Sub  
```  
  
### <a name="to-test-this-application"></a>Para probar esta aplicación  
  
1.  Guarde el esquema XSD de ejemplo en una carpeta.  
  
2.  Cree un proyecto ejecutable Visual Basic y copie el código en él. Modifique la ruta de acceso al directorio especificada según corresponda.  
  
3.  Agregue la siguiente referencia al proyecto:  
  
    ```  
    "Microsoft ActiveX Data Objects 2.8 Library"  
    ```  
  
4.  Ejecute la aplicación.  
  
 Éste es el resultado parcial:  
  
```  
<y0:Employee xmlns:y0="urn:myschema:Contacts"   
             LName="Achong" CID="1" FName="Gustavo"/>  
<y0:Employee xmlns:y0="urn:myschema:Employees"   
             LName="Abel" CID="2" FName="Catherine"/>  
```  
  
 Los prefijos que se generan en el documento XML son arbitrarios, pero se asignan al mismo espacio de nombres.  
  
  
