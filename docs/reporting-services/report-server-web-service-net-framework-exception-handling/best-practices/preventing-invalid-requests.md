---
title: "Impedir las solicitudes no válidas | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
caps.latest.revision: "32"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 527b27bc6a0af5195f167bb5ff7f0e84da027ef5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
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
  
 Para más información sobre los tipos de errores que se pueden evitar antes de que las solicitudes se envíen al servidor de informes, vea [Tabla de errores de SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Para más información sobre cómo mejorar más el ejemplo anterior mediante bloques try/catch, vea [Using Try and Catch Blocks (Uso de bloques Try y Catch)](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Ver también  
 [Introducción a la administración de excepciones en Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
