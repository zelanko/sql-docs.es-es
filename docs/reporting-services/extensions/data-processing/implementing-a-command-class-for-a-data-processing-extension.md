---
title: "Implementar una clase de comando para una extensión de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], commands
- Command class
- commands [Reporting Services]
ms.assetid: 465ef8d1-c503-407c-8afd-58d620e344ee
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9e6858a7f5c67508ff30396bb6ec668b908d671f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-command-class-for-a-data-processing-extension"></a>Implementar una clase Command para una extensión de procesamiento de datos
  El **comando** objeto formula una solicitud y lo pasa al origen de datos. El texto del comando puede adoptar muchos formatos sintácticos diferentes, como son texto y XML. Si se devuelven resultados, el **comando** objeto devuelve los resultados como un **DataReader** objeto.  
  
 Para crear un **comando** clase, implemente <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>. Implemente el <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> método para devolver un resultado se establece como un **DataReader** objeto. El <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> método de su **comando** clase debe incluir una implementación que tome un <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior> enumeración como argumento. Si implementa la extensión de procesamiento de datos para el Diseñador de informes, proporcione una implementación que administre un caso de <xref:Microsoft.ReportingServices.DataProcessing.CommandBehavior.SchemaOnly> en el método <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A>. Una implementación del esquema únicamente se utiliza para proporcionar una lista de campos al Diseñador de informes. El **DataReader** objeto devuelto por la <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand.ExecuteReader%2A> método debe contener información de tipo y el nombre de los campos o columnas, en el conjunto de resultados.  
  
 Si lo desea, su **comando** clase puede implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>. Esta interfaz permite que una clase de implementación analice una consulta y devuelva una lista de parámetros en la consulta. La funcionalidad de la interfaz <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> solo se utiliza en el Diseñador de informes. Al implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis>, se puede preguntar a los usuarios del Diseñador de informes los parámetros cada vez que un informe se ejecuta en el modo de vista previa. Además, puede ver los parámetros en la **parámetros** pestaña de la **conjunto de datos** cuadro de diálogo.  
  
> [!NOTE]  
>  No debería implementar <xref:Microsoft.ReportingServices.DataProcessing.IDbCommandAnalysis> si la extensión de procesamiento de datos personalizada no admite parámetros.  
  
 Para obtener un ejemplo **comando** implementación de la clase, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
