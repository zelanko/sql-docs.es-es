---
title: Ejecutar archivos de plantilla mediante el uso de la propiedad CommandStream | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Managed Classes [SQLXML], executing template files
- SQLXML Managed Classes, executing template files
- templates [SQLXML], SQLXML Managed Classes
- CommandStream property
ms.assetid: 55c564e3-56d1-4d85-bcaa-703e2905dd57
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d149b40acdc7fc81c79f8800787d093636753d39
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37331295"
---
# <a name="executing-template-files-by-using-the-commandstream-property"></a>Ejecutar archivos de plantilla utilizando la propiedad CommandStream
  En este ejemplo se muestra cómo se pueden especificar archivos de plantilla que están compuestos de consultas SQL o XPath utilizando la propiedad CommandStream del objeto SqlXmlCommand. En esta aplicación, se abre un FileStreamobject para un archivo de comandos y se asigna la secuencia de archivos como el CommandStream que se ejecuta.  
  
 En el ejemplo siguiente, se especifica la propiedad CommandType como SqlXmlCommandType.Template (no como TemplateFile).  
  
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
  
2.  Guarde el código C# (DocSample.cs) que se proporciona en este ejemplo en la misma carpeta donde se almacena el esquema. (Si almacena los archivos en otra carpeta, tendrá que modificar el código y especificar la ruta de acceso al directorio adecuada para el esquema de asignación).  
  
3.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DocSample.exe).  
  
4.  En el símbolo del sistema, ejecute DocSample.exe.  
  
  
