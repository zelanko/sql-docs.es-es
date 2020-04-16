---
title: Ejecute consultas SQL con el método ExecuteXMLReader
description: Aprenda a ejecutar consultas SQL mediante el método ExecuteXmlReader del objeto SqlXmlCommand para ejecutar comandos.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXML Managed Classes
- SQLXML Managed Classes, executing SQL queries
- Managed Classes [SQLXML], executing SQL queries
- ExecuteXmlReader method
- SQL queries [SQLXML]
ms.assetid: f106a4c5-8d6e-40c0-bf1f-11e121afcb01
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9acfa4eecb97902f20a0ba25762e2b14f2d5c756
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387999"
---
# <a name="executing-sql-queries-by-using-the-executexmlreader-method"></a>Ejecutar consultas SQL mediante el método ExecuteXMLReader
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En lugar de utilizar el método ExecuteToStream, puede usar el método ExecuteXmlReader del objeto SqlXmlCommand para ejecutar comandos. Este método devuelve un objeto XmlReader que se puede utilizar para el procesamiento posterior del resultado (que en este ejemplo es imprimir los nombres de elemento o atributo y los valores).  
  
> [!NOTE]  
>  En el código, debe proporcionar el nombre de la instancia de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
using System.Xml;  
   class Test  
   {  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks2012;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         SqlXmlParameter p;  
         XmlReader Reader;  
         XmlTextWriter tw;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.CommandText = "select FirstName, LastName from Person.Person where LastName = ? For XML Auto";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         Reader = cmd.ExecuteXmlReader();  
            tw = new XmlTextWriter(Console.Out);  
         Reader.MoveToContent();  
         tw.WriteNode(Reader, false);  
         tw.Flush();  
         tw.Close();  
         Reader.Close();  
  
         return 0;  
      }  
  
      static int Main(string[] args)  
      {  
         testParams();  
         return 0;  
      }  
   }  
```  
  
### <a name="to-test-the-application"></a>Para probar la aplicación  
  
1.  Asegúrese de que tiene [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework instalado en el equipo.  
  
2.  Guarde el código de C-(DocSample.cs) que se proporciona en este tema en una carpeta.  
  
3.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DocSample.exe).  
  
4.  En el símbolo del sistema, ejecute DocSample.exe.  
  
  
