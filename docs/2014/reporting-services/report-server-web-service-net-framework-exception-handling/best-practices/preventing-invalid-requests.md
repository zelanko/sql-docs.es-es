---
title: Impedir las solicitudes no válidas | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dcb850ad7e99768781b225978f531ff991766924
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158971"
---
# <a name="preventing-invalid-requests"></a>Impedir las solicitudes no válidas
  Puede impedir que se inicien algunos tipos de excepciones analizando el flujo de la aplicación y asegurándose de que las solicitudes que se van a enviar al servidor de informes son válidas. Por ejemplo, en las aplicaciones que permiten a los usuarios agregar o actualizar el nombre de un informe, origen de datos u otro elemento de servidor de informes, debería validar el texto que un usuario podría escribir. Siempre debería comprobar los caracteres reservados antes de enviar la solicitud a un servidor de informes. Use instrucciones **if** condicionales u otras construcciones lógicas en el código para avisar al usuario de que no se han cumplido las condiciones necesarias para enviar solicitudes al servidor de informes.  
  
 En el ejemplo de C# simplificado siguiente, se presenta a los usuarios un mensaje de error descriptivo cuando intentan crear un informe con un nombre que contiene un carácter de barra diagonal (/).  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 Para más información sobre los tipos de errores que se pueden evitar antes de que las solicitudes se envíen al servidor de informes, vea [Tabla de errores de SoapException](../soapexception-class/soapexception-errors-table.md). Para más información sobre cómo mejorar más el ejemplo anterior mediante bloques try/catch, vea [Using Try and Catch Blocks (Uso de bloques Try y Catch)](using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la administración de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
