---
title: Ejecutar consultas XPath con espacios de nombres (clases administradas de SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces property
- XPath queries [SQLXML], SQLXML Managed Classes
- queries [SQLXML], SQLXML Managed Classes
- XPath queries [SQLXML], namespaces
- Managed Classes [SQLXML], executing XPath queries
- SQLXML Managed Classes, executing XPath queries
- namespaces [SQLXML], XPath queries
ms.assetid: c6fc46d8-6b42-4992-a8f1-a8d4b8886e6e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d5e937cead8fa86fd249d782fa570639a403493
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015289"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxml-managed-classes"></a>Ejecutar consultas XPath con espacios de nombres (clases administradas de SQLXML)
  Las consultas XPath pueden incluir espacios de nombres. Si los elementos de esquema son espacios de nombres calificados (usan un espacio de nombres de destino), las consultas XPath que se realicen en el esquema deben especificar el espacio de nombres.  
  
 Dado que no se admite el uso del carácter comodín (*) en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, debe especificar la consulta XPath mediante un prefijo de espacio de nombres. Para resolver el prefijo, use la propiedad namespaces para especificar el enlace del espacio de nombres.  
  
 En el ejemplo siguiente, la consulta XPath especifica espacios de nombres mediante el carácter comodín ( \* ) y las funciones XPath de nombre local () y espacio de nombres-URI (). Esta consulta XPath devuelve todos los elementos en los que el nombre local es `Employee` y el URI del espacio de nombres es `urn:myschema:Contacts`:  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 En SQLXML 4.0, especifique esta consulta XPath con un prefijo de espacio de nombres. Un ejemplo sería `x:Contact`, donde `x` es el prefijo del espacio de nombres. Fíjese en el siguiente esquema XSD:  
  
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
  
 Dado que en este esquema se define el espacio de nombres de destino, una consulta XPath (como "Employee") en este esquema debe incluir el espacio de nombres.  
  
 La aplicación de ejemplo C# siguiente ejecuta una consulta XPath en el esquema XSD anterior (MySchema.xml). Para resolver el prefijo, especifique el enlace de espacio de nombres mediante la propiedad namespaces del objeto SqlXmlCommand.  
  
> [!NOTE]  
>  En el código, debe suministrarse el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testXPath()  
      {  
         //Stream strm;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "x:Contact[@CID='1']";  
         cmd.CommandType = SqlXmlCommandType.XPath;  
         cmd.RootTag = "ROOT";  
         cmd.Namespaces = "xmlns:x='urn:myschema:Contacts'";  
         cmd.SchemaPath = "MySchema.xml";  
         using (Stream strm = cmd.ExecuteStream()){  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
      public static int Main(String[] args)  
      {  
         testXPath();  
         return 0;  
      }  
   }  
```  
  
 Para probar este ejemplo, debe tener instalado [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework en el equipo.  
  
### <a name="to-test-the-application"></a>Para probar la aplicación  
  
1.  Guarde el esquema XSD (MySchema.xml) que se proporciona en este ejemplo en una carpeta.  
  
2.  Guarde el código C# (DocSample.cs) que se proporciona en este ejemplo en la misma carpeta en la que se almacena el esquema. (Si almacena los archivos en otra carpeta, tendrá que modificar el código y especificar la ruta de acceso al directorio adecuada para el esquema de asignación).  
  
3.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DocSample.exe).  
  
4.  En el símbolo del sistema, ejecute DocSample.exe.  
  
  
