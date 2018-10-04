---
title: Procesamiento XML en el lado cliente (clases administradas de SQLXML) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- processing XML on client side [SQLXML]
- client-side XML formatting
- Managed Classes [SQLXML], client-side XML formatting
- SQLXML Managed Classes, client-side XML formatting
- ClientSideXml property
ms.assetid: 5e7ecf18-66fc-49ff-bc50-83635cd7ac0b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 82344c8ab1b83fab957ac1b734bfb8d11cbcd3c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179655"
---
# <a name="processing-xml-on-the-client-side-sqlxml-managed-classes"></a>Procesar XML en el cliente (clases administradas de SQLXML)
  En este ejemplo se muestra el uso de la clientsidexml, propiedad. La aplicación ejecuta un procedimiento almacenado en el servidor. El resultado del procedimiento almacenado (un conjunto de filas de dos columnas) se procesa en el cliente para generar un documento XML.  
  
 El siguiente GetContacts procedimiento almacenado devuelve **FirstName** y **LastName** de los empleados de la tabla Person.Contact de la base de datos AdventureWorks.  
  
```  
USE AdventureWorks  
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 Esta aplicación de C# ejecuta el procedimiento almacenado y especifica la opción FOR XML AUTO en especificando el valor CommandText. En la aplicación, el clientsidexml, propiedad del objeto SqlXmlCommand se establece en true. Esto le permite ejecutar procedimientos almacenados preexistentes que devuelven un conjunto de filas y aplican a este último una transformación XML en el cliente.  
  
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
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
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
  
 Para probar este ejemplo, debe tener instalado [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework en el equipo.  
  
### <a name="to-test-the-application"></a>Para probar la aplicación  
  
1.  Cree el procedimiento almacenado.  
  
2.  Guarde el código (DocSample.cs) de C# que se proporciona en este ejemplo en una carpeta. Modifique el código para especificar la información adecuada de inicio de sesión y contraseña.  
  
3.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DocSample.exe).  
  
4.  En el símbolo del sistema, ejecute DocSample.exe.  
  
  
