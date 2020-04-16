---
title: Ejecute archivos de plantilla con la propiedad CommandStream
description: Aprenda a ejecutar archivos de plantilla que constan de consultas SQL o XPath mediante la propiedad CommandStream del objeto SqlXmlCommand.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a3b7922921c64c9afb7ef37be57db23a32470eaf
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388364"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>Ejecutar archivos de plantilla utilizando la propiedad CommandStream
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este ejemplo se muestra cómo se pueden especificar los archivos de plantilla que constan de consultas SQL o XPath mediante la propiedad CommandStream del objeto SqlXmlCommand. En esta aplicación, se abre un objeto FileStream para un archivo de comandos y la secuencia de archivos se asigna como CommandStream que se ejecuta.  
  
 En el ejemplo siguiente, la propiedad CommandType se especifica como SqlXmlCommandType.Template (no como TemplateFile).  
  
 Esta es la plantilla XML de ejemplo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
    SELECT TOP 2 ContactID, FirstName, LastName   
    FROM   Person.Contact  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Esta es la aplicación C# de ejemplo. Para probar la aplicación, guarde la plantilla (TemplateFile.xml) y, a continuación, ejecute la aplicación. La aplicación ejecuta la consulta especificada en la plantilla XML y muestra el documento XML generado en pantalla.  
  
> [!NOTE]  
>  En el código, debe proporcionar el nombre de la instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         MemoryStream ms = new MemoryStream();  
         StreamWriter sw = new StreamWriter(ms);  
         ms.Position = 0;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandStream = new FileStream("TemplateFile.xml", FileMode.Open, FileAccess.Read);  
         cmd.CommandType = SqlXmlCommandType.Template;  
         using (Stream strm = cmd.ExecuteStream())  
         {  
            using (StreamReader sr = new StreamReader(strm)){  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;        
      }  
  
      public static int Main(String[] args)  
      {  
         testParams();     
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>Para probar la aplicación  
  
1.  Guarde la plantilla XML (TemplateFile.xml) que se proporciona en este ejemplo en una carpeta.  
  
2.  Guarde el código de C-(DocSample.cs) que se proporciona en este ejemplo en la misma carpeta en la que se almacena el esquema. (Si almacena los archivos en otra carpeta, tendrá que modificar el código y especificar la ruta de acceso al directorio adecuada para el esquema de asignación).  
  
3.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DocSample.exe).  
  
4.  En el símbolo del sistema, ejecute DocSample.exe.  
  
  
